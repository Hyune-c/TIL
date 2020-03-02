# Annotation

## @RequestBody vs @RequestParam vs @PathVariable


## javax.validation 빈 검증
|            | @Notnull      | @NotEmpty     | @NotBlank     |
| :--------- | :------------ | :------------ | ------------- |
| null       | 허용하지 않음 | 허용하지 않음 | 허용하지 않음 |
| ""         | 허용          | 허용하지 않음 | 허용하지 않음 |
| " "(space) | 허용          | 허용          | 허용하지 않음 |
