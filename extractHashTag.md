# 문자열에서 해쉬태그 추출하기

```java
	public List<String> extractHashTag(String message) {
		List<String> tagList = new ArrayList<>();
		Pattern p = Pattern.compile("\\#([0-9a-zA-Z가-힣]*)");
		Matcher m = p.matcher(message);
		String extractHashTag;

		while (m.find()) {
			extractHashTag = replaceSpecialCharacter(m.group());
			if (extractHashTag != null) {
				tagList.add(extractHashTag);
//				System.out.println("hash tag :: " + extractHashTag);
			}
		}
		return tagList;
	}

	public String replaceSpecialCharacter(String s) {
		s = StringUtils.replaceChars(s, "-_+=!@#$%^&*()[]{}|\\;:'\"<>,.?/~`） ", "");
		if (s.length() < 1) {
			return null;
		}
		return s;
	}
```
