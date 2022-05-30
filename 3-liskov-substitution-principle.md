<h1>Liskov substitution principle</h1>
<p>O princípio de substituição de Liskov diz que quando você tem uma classe <b>BASE</b> ela pode ser <b>SUBSTITUÍDA</b> por uma classe <b>DERIVADA</b>, pois a classe <b>DERIVADA</b> também é uma classe <b>BASE</b>.</p>

<p>Agora você deve estar pensando "max que m&rd@ isso quer dizer?"</p>

<p>Imagine que temos uma classe <b>BASE</b> chamada `PostgresRepository.ts` com apenas três métodos (três são o exemplo, na verdade você pode ter quantos forem necessários).</p>

```
class PostgresRepository {

}

export { PostgresRepository };
```

<p>Porem para que a nossa classe <b>BASE</b> possa ser <b>SUBSTITUÍDA</b> por uma classe <b>DERIVADA</b> devemos adicionar um <b>CONTRATO</b>. Neste caso como estamos utilizando TypeScript utilizaremos uma interface como contrato.</p>

```
interface IDatabaseRepository {
  findByName(name: string): string;
  list(): string[];
  create(name: string): void;
}

export { IDatabaseRepository };
```

<p>Agora vamos implementar este contrato em nossa classe <b>BASE</b>.</p>

```
import { IDatabaseRepository } from './IDatabaseRepository';

class PostgresRepository implements IDatabaseRepository {

}

export { PostgresRepository };
```

<p>Se você estiver utilizando o Visual Studio Code provavelmente ele ira reclamar que os nossos três métodos não foram adicionar a classe `PostgresRepository`. Vamos adicionar os nossos três métodos agora.</p>

```
import { IDatabaseRepository } from './IDatabaseRepository';

class PostgresRepository implements IDatabaseRepository{
  findByName(name: string): string {
    console.log(name);
    return null;
  }

  list(): string[] {
    console.log('lista');
    return null;
  }

  create(name: string): void {
    console.log(name);
  }
}

export { PostgresRepository };
```

<p>Agora nossa classe PostgresRepository está com o contrato assinado com a nossa interface. Porem agora precisamos da nossa classe <b>DERIVADA<b/>. Vamos criá-lá.</p>
  
```
class MysqlRepository {

}

export { MysqlRepository };
```
  
<p>Agora vamos implementar nosso contrato em nossa classe <b>DERIVADA</b>.</p>

```
import { IDatabaseRepository } from './IDatabaseRepository';

class MysqlRepository implements IDatabaseRepository {

}

export { MysqlRepository };
```

<p>Não podemos nos esquecer de assinar está classe também com os métodos do contrato.</p>

```
import { IDatabaseRepository } from './IDatabaseRepository';

class MysqlRepository implements IDatabaseRepository {
  findByName(name: string): string {
    console.log(name);
    return null;
  }

  list(): string[] {
    console.log('lista');
    return null;
  }

  create(name: string): void {
    console.log(name);
  }
}

export { MysqlRepository };
```

<p>Beleza, agora vamos criar uma rota de POST para utilizarmos nossa classe <b>BASE</b> e <b>DERIVADA</b>. Para criarmos a rota vomos utilizar o Express.</p>

```
import { Router } from 'express';

import { PostgresRepository } from './PostgresRepository';

const routes = Router();
const repository = new PostgresRepository();

routes.post('/users', (req, res) => {
  const { name } = req.body;

  const createUserService = new CreateUserService(repository);

  createUserService.execute(name);

  return res.status(201).send();
});
```

<p>E também vamos criar nossa classe `CreateUserService` com o método `execute` dentro dela.</p>




























