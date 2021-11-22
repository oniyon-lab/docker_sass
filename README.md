# docker_sass

## 前提条件
Macでdockerが動く環境を用意してください

## dockerでsassを変換してくれるシェルを用意します
1. 下記の様なシェルスクリプトを作ります。  
sass.sh
```
#!/bin/bash

docker pull orianna/dart-sass

docker run -it --rm -v $(pwd):/sass -v $(pwd):/output orianna/dart-sass:latest $1 ${1%.*}.css
```

2. シェルスクリプトのパーミッションを変更し実行できるようにします
```
chmod 700 sass.sh
```

## sassファイルを用意し、変換してみます
3. 下記の様なsassを用意してみます。  
test.scass
```
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

4. 変換を実行  
```
./sass.sh test.scass
```

5. test.cssが出力されている。中身確認  
test.css
```
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}

/*# sourceMappingURL=test.css.map */
```

![image](https://user-images.githubusercontent.com/2200168/142796758-cbc48479-9500-41c0-8b11-0839fed830a9.png)
