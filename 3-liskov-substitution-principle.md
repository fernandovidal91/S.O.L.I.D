<h1>Liskov substitution principle</h1>
<p>O princípio de substituição de Liskov diz que quando você tem uma classe <b>BASE</b> ela pode ser <b>SUBSTITUÍDA</b> por uma classe <b>DERIVADA</b>, pois a classe <b>DERIVADA</b> também é uma classe <b>BASE</b>.</p>

<p>Agora você deve estar pensando "max que m&rd@ isso quer dizer?"</p>

<p>Imagine que temos uma classe <b>BASE</b> chamada `PostgresRepository.ts` com apenas três métodos (três são o exemplo, na verdade você pode ter quantos forem necessários).</p>

```
class PostgresRepository {

}

export default new PostgresRepository();
```

<p>Porem para que a nossa classe <b>BASE</b> possa ser <b>SUBSTITUÍDA</b> por uma classe <b>DERIVADA</b> devemos adicionar um <b>CONTRATO</b>. Neste caso como estamos utilizando TypeScript utilizaremos uma interface como contrato.</p>

```
interface IUserRepository {
  findByName(name: string): string;
  list(): string[];
  create(name: string): void;
}

export default IUserRepository;
```
