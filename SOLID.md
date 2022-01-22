# SOLID

S - (Princípio da responsabilidade única)<br />
O - (Princípio aberto-fechado)<br />
L - (Princípio da substituição de liskov)<br />
I - (Princípio da segregação da Interface)<br />
D - (Princípio da inversão da Dependência)<br />

## Princípio da responsabilidade única

Uma classe deve ser especializada em um único assunto, e possuir uma responsabilidade dentro do software, ou seja, a classe deve possuir uma única tarefa ou ação para executar.

```
// Maneira errada de usar SOLID
```
```
// Maneira certa de usar SOLID

class Order {
  public function calculateTotalSum() {}
  public function getItems() {}
  public function getItemCount() {}
  public function addItem() {}
  public function deleteItem() {}
}

class OrderRepository {
  public function load(orderId) {}
  public function save(order) {}
  public function update(order) {}
  public function delete(order) {}
}

class OrderViewer {
  public function printOrder(order) {}
  public function showOrder(order) {}
}
```

## Princípio aberto-fechado

Os objetos ou entidades devem estar abertos para extenção mas fechados para modificação. Quando um novo comportamento e recursos precisam ser adicionados no software devemos extender e não alterar o código font original.

```
 class ContratoClt {
   public function salario() {}
 }

 class Estagio {
   public function bolsaAuxilio() {}
 }

 class FolhaDePagamento {
   protected $saldo;

   public function calcular($contrato) {
     if ($contrato instanceof ContratoClt) {
       $this->saldo = $contrato->salario();
     } else if ($contrato instanceof Estagio) {
       $this->saldo = $contrato->bolsaAuxilio();
     }
   }
 }
```

```
  interface Remuneravel() {
    public function remuneracao();
  }

  class ContratoClt implements Remuneravel {
    public function remuneracao() {}
  }

  class ContratoPj implements Remuneravel {
    public function remuneracao() {}
  }

  class Estagio implements Remuneravel {
    public function remuneracao() {}
  }

  class FolhaDePagamento {
    protected $saldo;

    public function calcular(Remuneravel $contrato) {
      $this->saldo = $contrato->remuneracao();
    }
  }
```
