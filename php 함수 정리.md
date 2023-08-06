## php 함수
### sprintf() - 형식화된 문자열 반환
- %% : 백분율 기호로 반환
- %d : 부호 있는 10진수 (음수, 0 또는 양수)
- %02d: 한자리 숫자에 0을 붙여서 01,02,03,04 ... 로 만드는 방법
```php
sprintf(string $format, mixed ...$values): string
```
```php
//사용 예제
$idx = (($i > 23) ? sprintf('%02d', ($i - 24)) : sprintf('%02d', $i));
```

---
### explode() - 문자열을 분할해서 문자열의 배열을 반환
- separator : 문자열을 분할할 기준
- string : 분할할 문자열
- limit : 옵션으로, 분할할 개수 정함, 정수 입력
```php
explode(string $separator, string $string, int $limit = PHP_INT_MAX): array
```
```php
//사용 예제
$code_name_split = explode("~", $tmp_obj['code_name']);
```

---
### implode() - 배열을 하나의 문자열로 반환
- separator : 배열의 원소 사이에 들어갈 문자열
- array : 배열
```php
implode(string $separator, array $array): string
```
```php
//사용 예제
$code_column = implode("','", $code);
```

---
### array_push() - 하나 이상의 요소를 배열 끝에 푸시
- array : 추가할 배열
- mixed : 추가하는 데이터
```php
array_push(array &$array, mixed ...$values): int
```
```php
//사용 예제
array_push($arr_row_data, $object);
```

---
### count() - 배열과 객체의 모든 엘리먼트의 개수를 계산하여 숫자로 반환
```php
count(Countable|array $value, int $mode = COUNT_NORMAL): int
```
```php
//사용 예제
count($code)
```