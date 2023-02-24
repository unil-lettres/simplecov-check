# SimpleCov Check

A simple action that can pass/fail your build in an isolated job based on the results of a SimpleCov report.

## Usage
```yml
jobs:
  # Your test job should include something like the following
  test:
    runs-on: ubuntu-latest

    - name: Run specs
      run: bundle exec rspec

    - name: Upload coverage results
      uses: actions/upload-artifact@v3
      with:
        name: coverage-report
        path: coverage

  coverage:
    runs-on: ubuntu-latest

    # This line will only run the coverage job if the test job passed
    needs: test

    steps:
    - name: Download coverage report
      uses: actions/download-artifact@v3
      with:
        name: coverage-report
        path: coverage

    - name: Check coverage
      uses: unil-lettres/simplecov-check@main
      with:
        minimum_coverage: 100
        coverage_path: coverage/.last_run.json
```
