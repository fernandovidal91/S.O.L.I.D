# Open-closed Principle

#### No nosso exemplo teremos duas entidades, uma de professor e outra de aluno, porém ambas são pessoas. Isso quer dizer que ambas têm nome, idade e altura. Porém, há particularidades de cada uma das entidades.
#### Um exemplo de particularidades é: Aluno tem as notas dele. E o professor tem o nome da matéria que ele leciona.

```
class Pessoa {
  nome: string;
  idade: number;
  altura: number;
  
  constructor(nome: string, idade: number, altura: number) {
    this.nome = nome;
    this.idade = idade;
    this.altura = altura;
  }
  
  getNome() {
   return this.nome;
  }
  
  getIdade() {
    return this.idade;
  }
  
  getAltura() {
    return this.altura;
  }
}

class Professor extends Pessoa {
  materia: string;
  
  constructor(nome: string, idade: number, altura: number, materia: string) {
    super(nome, idade, altura);
    this.materia = materia;
  }
  
  getMateria() {
    return this.materia;
  }
}

class Aluno extends Pessoa {
   constructor(nome: string, idade: number, altura: number, private notas: number[]) {
    super(nome, idade, altura);
  }
  
  getNotas() {
    return this.notas;
  }
}
```
