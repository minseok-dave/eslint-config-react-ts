## ci.settings

eslint가 적용되려면 아래처럼 따라해주세요.

1. src 폴더와 동일한 위치에서 .vscode 폴더를 생성합니다.
2. .vscode 폴더 안에 settings.json 파일을 생성합니다.
3. settings.json 파일에 아래 코드를 복사 붙여넣기를 합니다.

```
{
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    },
    "files.exclude": {
      "**/.git": true,
      "**/.svn": false,
      "**/.hg": false,
      "**/CVS": false,
      "**/.DS_Store": false,
      "**/Thumbs.db": false,
      "**/node_modules": true
    },
    "explorerExclude.backup": {},
    "tailwindCSS.experimental.classRegex": [
      ["cva\\(([^)]*)\\)", "[\"'`]([^\"'`]*).*?[\"'`]"]
    ]
}

```

4. 또한 동일한 위치에 extensions.json 파일을 생성합니다.
5. extensions.json 파일에 아래 코드를 복사 붙여넣기를 합니다.

```
{
    "recommendations": [
        "csstools.postcss",
        "formulahendry.auto-rename-tag",
        "dbaeumer.vscode-eslint",
        "peterschmalfeldt.explorer-exclude",
        "eamodio.gitlens",
        "pkief.material-icon-theme",
        "codeandstuff.package-json-upgrade",
        "esbenp.prettier-vscode",
        "jock.svg",
        "bradlc.vscode-tailwindcss",
        "austenc.tailwind-docs",
        "meganrogge.template-string-converter",
        "wayou.vscode-todo-highlight"
    ]
}

```

6. 다음은 .eslintrc.cjs 파일입니다. 이 파일에서 아래 코드처럼 extends에 패키지를 추가합니다.

```
module.exports = {
  root: true,
  extends: ['@beloved-diver/eslint-config-react']
}

```

7. 프로그램을 종료했다가 다시 켭니다.
8. 권장 설치 확장앱을 설치하시겠느냐 물으면, 모두 설치합니다. 혹은 eslint와 prettier를 설치해주시면 됩니다.
9. command + f1을 눌러 커맨드창을 열고, restart Eslint server을 선택합니다.
10. eslint가 올바르게 적용되는지 확인합니다.

## Window 유저일 경우 위의 대로 했는데, 에러가 발생할 수 있습니다.
만약 에러가 발생했다면,

rules에 아래 코드를 추가합니다.

```
rules: {
    'prettier/prettier': [
    'error',
    {
      printWidth: 100, // 한 줄에 출력할 수 있는 최대 문자 수를 100개로 설정
      semi: false, // 세미콜론을 사용하지 않도록 설정
      singleQuote: true, // 문자열을 작은따옴표로 표시
      tabWidth: 2, // 탭 문자의 너비를 2로 설정
      trailingComma: 'all', // 여러 줄로 구성된 배열 또는 객체 리터럴의 마지막 요소 뒤에 항상 쉼표를 사용하도록 설정
    },
  ],
}

```



## tailwindcss 

이 eslint에는 tailwindcss config가 포함되어 있어요!

정의하지 않은 className을 선언하면, eslint에서 Error를 표시하게 되는데,
이를 방지하려면 eslintrc.cjs에 아래 코드를 작성해야합니다.

cssFiles는 tailwindcss가 작성된 css 파일입니다. 즉 App Component에서 import한 파일입니다.
whitelist는 ignore에 추가될 class 이름입니다.

만약에 btn이라는 이름으로 class 이름을 정의했다면,
아래 예시 처럼 될 것입니다.

```
rules: {
    'tailwindcss/no-custom-classname': [
      'error',
      {
        cssFiles: ['src/style.css'],
        whitelist: [
          'btn',
        ],
      },
    ],
},

```