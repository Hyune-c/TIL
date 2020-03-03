# Annotation

## @RequestBody vs @RequestParam vs @PathVariable


## javax.validation 빈 검증
> 실제 DB 에는 모두 not null 로 들어갑니다.

|            | @Notnull      | @NotEmpty     | @NotBlank     |
| :--------- | :------------ | :------------ | ------------- |
| null       | 허용하지 않음 | 허용하지 않음 | 허용하지 않음 |
| ""         | 허용          | 허용하지 않음 | 허용하지 않음 |
| " "(space) | 허용          | 허용          | 허용하지 않음 |
