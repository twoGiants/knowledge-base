# Tekton

## Tests

- Q: Do you prefer public API tests or package scope tests?
  - A: Public where possible, private case by case if not possible otherwise.
- Q: Do you prefer integration tests testing multiple components together or each piece on its own?
  - A: Test coverage must stay high, prefer integration tests over piece by piece.
- Q: Should tests be moved/extracted when you decompose functions or components?
  - A: If coverage does not change no need to extract tests.
