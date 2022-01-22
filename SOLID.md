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

```














