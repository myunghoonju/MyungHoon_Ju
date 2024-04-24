#### Compound name
한눈에 들어오는 간단한 내용에서는 한글자도 유추가 가능하면 OK
```java
    // i는 아마도 index? 
    public static void main(String[] args) {
    List<Integer> list = List.of(1, 2, 3);
    for (int i = 0; i < 1; i++) {
        System.out.println(list.get(i));
    }
}
```
> 서술적인 변수명을 사용하는 근본적인 이유는? -> 한단어로 이해가 어렵기 때문    
> 이름보다 중요한 것은 한글자라도 유추 가능하도록 읽기 쉬운 코드를 작성하는 것  
> 코드의 복잡도가 높아질 수록 우리는 길고 서술적인 변수명을 사용하게 되는 것  

> 코드의 이해를 위해서 변수명을 가지고 설명이 필요하다면 리팩터링이 필요하다는 신호 

> 한단어로 표현이 가능하도록 프로그래밍하면 OK  
> 형용사 사라지면 어색한 이름들의 경우 제외 -> washingMachine, MicroService

```java
    // from java 17
    // 서술적인 변수명을 사용하였다... 이제 이해하기 쉬운 내용인가?  
    static int lastIndexOf(byte[] src, byte srcCoder, int srcCount,
                           String tgtStr, int fromIndex) {
        byte[] tgt = tgtStr.value;
        byte tgtCoder = tgtStr.coder();
        int tgtCount = tgtStr.length();
        /*
         * Check arguments; return immediately where possible. For
         * consistency, don't check for null str.
         */
        int rightIndex = srcCount - tgtCount;
        if (fromIndex > rightIndex) {
            fromIndex = rightIndex;
        }
        if (fromIndex < 0) {
            return -1;
        }
        /* Empty string always matches. */
        if (tgtCount == 0) {
            return fromIndex;
        }
        if (srcCoder == tgtCoder) {
            return srcCoder == LATIN1
                ? StringLatin1.lastIndexOf(src, srcCount, tgt, tgtCount, fromIndex)
                : StringUTF16.lastIndexOf(src, srcCount, tgt, tgtCount, fromIndex);
        }
        if (srcCoder == LATIN1) {    // && tgtCoder == UTF16
            return -1;
        }
        // srcCoder == UTF16 && tgtCoder == LATIN1
        return StringUTF16.lastIndexOfLatin1(src, srcCount, tgt, tgtCount, fromIndex);
    }
```

> 설명도 충분히 들었으니 아무 코드에 적용해볼까?

```java
   // from java 17
   // original
    public static String quote(String s) {
    int slashEIndex = s.indexOf("\\E");
    if (slashEIndex == -1)
        return "\\Q" + s + "\\E";

    int lenHint = s.length();
    lenHint = (lenHint < Integer.MAX_VALUE - 8 - lenHint) ?
              (lenHint << 1) : (Integer.MAX_VALUE - 8);

    StringBuilder sb = new StringBuilder(lenHint);
    sb.append("\\Q");
    int current = 0;
    do {
        sb.append(s, current, slashEIndex)
          .append("\\E\\\\E\\Q");
        current = slashEIndex + 2;
    } while ((slashEIndex = s.indexOf("\\E", current)) != -1);

    return sb.append(s, current, s.length())
             .append("\\E")
             .toString();
   }

    // refactored
    public static String quote(String s) {
        int i = s.indexOf("\\E");
        if (i == -1) {
            return "\\Q" + s + "\\E";
        }

        StringBuilder sb = new StringBuilder(length(s));
        int begin = begin(s, sb, i);
        int end = s.length();
        
        return sb.append("\\Q")
                 .append(s, begin, end)
                 .append("\\E")
                 .toString();
    }

    private static int length(String s) {
        int lenHint = s.length();
        lenHint = (lenHint < Integer.MAX_VALUE - 8 - lenHint) ? 
                  (lenHint << 1) : (Integer.MAX_VALUE - 8);
        return lenHint;
    }

    private static int begin(String s, StringBuilder sb, int slashEIndex) {
        int current = 0;
        do {
            sb.append(s, current, slashEIndex).append("\\E\\\\E\\Q");
            current = slashEIndex + 2;
        } while ((slashEIndex = s.indexOf("\\E", current)) != -1);
        return current;
    }

    public static void main(String[] args) {
        String dollarAmounts = "$100.25, $100.50, $150.50, $100.50, $100.75";
        String patternStr = "$100.50";
        
        //Pattern pattern = Pattern.compile(Pattern.quote(patternStr));        
        Pattern pattern = Pattern.compile(quote(patternStr));
        Matcher matcher = pattern.matcher(dollarAmounts);

        int matches = 0;
        while (matcher.find()) {
            matches++;
        }

        System.out.println(matches); // 2
    }
```
> quote()는 조금 더 읽기 쉬워졌을까?