<h1>Liskov substitution principle</h1>
<p>O princípio de substituição de Liskov diz que quando você tem uma classe <b>BASE</b> ela pode ser <b>SUBSTITUÍDA</b> por uma classe <b>DERIVADA</b>, pois a classe <b>DERIVADA</b> também é uma classe <b>BASE</b>.</p>

<p>Agora você deve estar pensando "mas que m&rd@ isso quer dizer?"</p>

<p>Imagine que temos uma classe <b>BASE</b> chamada PostgresRepository.ts com apenas três métodos (três são o exemplo, na verdade você pode ter quantos forem necessários).</p>

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

<p>Se você estiver utilizando o Visual Studio Code provavelmente ele ira reclamar que os nossos três métodos não foram adicionar a classe PostgresRepository. Vamos adicionar os nossos três métodos agora.</p>

```
import { IDatabaseRepository } from './IDatabaseRepository';

class PostgresRepository implements IDatabaseRepository{
  findByName(name: string): string {
    console.log('Você utilizou o método findByName da classe PostgresRepository.');
    return name;
  }

  list(): string[] {
    console.log('Você utilizou o método list da classe PostgresRepository.');
    return [name, name, name];
  }

  create(name: string): void {
    console.log('Você utilizou o método create da classe PostgresRepository.');
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
    console.log('Você utilizou o método findByName da classe MysqlRepository.');
    return null;
  }

  list(): string[] {
    console.log('Você utilizou o método list da classe MysqlRepository.');
    return null;
  }

  create(name: string): void {
    console.log('Você utilizou o método create da classe MysqlRepository.');
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

<p>E também vamos criar nossa classe CreateUserService com o método execute dentro dela.</p>

```
class CreateUserService {
  execute(name: string): void {
    
  }
}

export { CreateUserService };
```

<p>Okay, aqui esta o pulo do gato. Primeiro vamos criar uma váriavel privada com o nome de repository que sera do mesmo tipo que o nosso <b>CONTRATO</b>. Também vamos receber a nossa classe <b>BASE</b> ou a nossa classe <b>DERIVADA</b> no contrutor. Calma, já irei te explicar por que iremos receber a nossa classe <b>BASE</b> ou a nossa classe <b>DERIVADA</b> no contrutor</p>.

```
import { IDatabaseRepository } from './IDatabaseRepository';

class CreateUserService {
  private repository: IDatabaseRepository;
  
  constructor(repository: IDatabaseRepository) {
    this.repository = repository;
  }

  execute(name: string): void {
    
  }
}

export { CreateUserService };
```

<p>Aqui nos criamos uma váriavel repository que é do tipo IDatabaseRepository e recebemos nossa classe <b>BASE</b> ou <b>DERIVADA</b> no construtor colocando ela dentro da nossa váriavel repository. Agora vamos escrever um pouco de código dentro do nosso método execute.</p>

```
import { IDatabaseRepository } from './IDatabaseRepository';

class CreateUserService {
  private repository: IDatabaseRepository;
  
  constructor(repository: IDatabaseRepository) {
    this.repository = repository;
  }

  execute(name: string): void {
    const userAlreadyExists = this.repository.findByName(name);
    
    if (categoryAlreadyExists) {
      throw new Error('Category already exists');
    }
    
    this.repository.create(name);
  }
}

export { CreateUserService };
```

<p>Pronto, agora se você testar tudo estará certo e no seu console deve estar aparecendo as seguintes mensagens.</p>

```
Você utilizou o método findByName da classe PostgresRepository.
Você utilizou o método create da classe PostgresRepository.
```
















