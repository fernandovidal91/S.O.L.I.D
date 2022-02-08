# Single Responsibility Principle

#### Digamos que temos uma entidade Livro e precisamos inseri-lo no banco de dados. No exemplo sem usar este princípio nós criaríamos uma classe Livro e toda a implementação, inclusive o insert no banco de dados, estaria dentro dela.

#### Sendo assim, a classe Livro teria duas responsabilidades, a primeira de conter as informações a respeito do livro, e a segunda de se conectar com o banco e inseri-lo.

```
// Esta classe não segue o princípio da responsabilidade única

class Livro {
  private database: Database;
  
  constructor(private titulo: string, private resumo: string){
    const db = new DatabaseInstance();
    this.database = db.connect("connectionstring", ["livros"]);
  }
  
  getTitulo() {
    return this.titulo;
  }
  
  save() {
    this.database.livros.save({
      titulo: this.titulo,
      resumo: this.resumo
    })
  }
}
```

#### Na forma correta de implementar, nós temos duas classes separadas. Uma especificamente focada em tratar a entidade livro e a outra sendo um repositório, que fará todas as interações com o banco de dados. Sendo assim, cadas classe tem uma responsabilidade única, como o princípio manda.

```
class Livro {
  constructor(private titulo: string, private resumo: string){}
  
  getTitulo() {
    return this.titulo;
  }
  
  getResumo() {
    return this.resumo;
  }
}

class LivroRepository {
  private database: Database;
  
  constructor(){
    const db = new DatabaseInstance();
    this.database = db.connect("connectionstring", ["livros"]);
  }
  
  save(livro: Livro) {
    this.database.livros.save({
      titulo: livro.getTitulo(),
      resumo: livro.getResumo(),
    })
  }
}
```




