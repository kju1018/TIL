# Java Design Pattern-Builder

- 구조가 가지고 있는 큰 것을 구축한다.
- 복잡한 구조를 가지는 것을 만들 때 한번에 완성하는 것은 어렵다. 구조를 이루는 각 부품을 하나씩 만들어 가는 방법

## 코드

```
package com.company.builder;

public class Text {
    private String text;

    @Override
    public String toString() {
        return text;
    }

    public static class Builder {
        private String title;
        private String content;
        private String[] items;

        public Builder setTitle(String title){
            this.title = title;
            return this;
        }

        public Builder setContent(String content){
            this.content = content;
            return this;
        }
        //가변인자 갯수에 상관없이 받음음
       public Builder setItems(String ... items){
            this.items = items;
            return this;
        }

        public Text build(){
            Text text = new Text();

            StringBuilder sb = new StringBuilder();
            sb.append("타이틀 = ").append(title).append("\\n");
            sb.append("내용: ").append(content).append("\\n");
            sb.append("항목: ").append("\\n");
            for(String item : items){
                sb.append(" - ").append(item).append("\\n");
            }

            text.text = sb.toString();

            return text;
        }

    }
}
public class Main {

    public static void main(String[] args) {
        Text text = new Text.Builder()
                .setTitle("hello")
                .setContent("내용")
                .setItems("항목1", "항목2", "항목3")
                .build();

        System.out.println(text);

    }
}
```

## 결과

```
타이틀: 제목
내용: 내용
항목:

- 항목1
- 항목2
- 항목3
```

## 메리트

코드 읽기/유지보수가 편하다.

객체 생성을 깔끔하게 할 수 있다.