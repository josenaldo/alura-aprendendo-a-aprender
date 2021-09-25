# Aprenendo a aprender

Anotações do Curso curso Aprendendo a Aprender, da Alura.

## Atenção

Por enquanto, o [StackEdit](https://stackedit.io/) está tendo problemas para processar a autenticação do Github. Até que esse problema seja resolvido, segue a gambiarra fornecida pelo usuário [@mogoe](https://github.com/benweet/stackedit/issues/1755#issuecomment-918949789):

> Once you are on the screen asking you to "Grant access to your private
> repositories," open the developer console and paste the following
> lines.

```js
window.XMLHttpRequest =  class MyXMLHttpRequest extends window.XMLHttpRequest {
  open(...args){
    if(args[1].startsWith("https://api.github.com/user?access_token=")) {
      // apply fix as described by github
      // https://developer.github.com/changes/2020-02-10-deprecating-auth-through-query-param/#changes-to-make
  
      const segments = args[1].split("?");
      args[1] = segments[0]; // remove query params from url
      const token = segments[1].split("=")[1]; // save the token
      
      const ret = super.open(...args);
      
      this.setRequestHeader("Authorization", `token ${token}`); // set required header
      
      return ret;
    }
    else {
      return super.open(...args);
    }
  }
}
```



<!--stackedit_data:
eyJoaXN0b3J5IjpbNTkzMjA2Mzg0LDE1MDQ3MTY2MDAsLTIwMj
k1MjEzNDldfQ==
-->