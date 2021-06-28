# Бинарное дерево

**Бинарное дерево** представляет собой структуру данных дерева, в котором каждый узел имеет не более двух детей, 
которые переданы в качестве *левого ребенка* и *права ребенка*. 

**Обход дерева** - это процесс посещения (проверки или обновления) каждого узла в структуре данных дерева ровно один раз. 
В отличие от связанных списков или одномерных массивов, которые канонически просматриваются в линейном порядке, деревья 
можно обходить разными способами. Они могут проходить по порядку, в глубину или в ширину .

Есть три распространенных способа пройти по дереву в порядке глубины:
1. In-order
2. Pre-order
3. Post-order

## 1. Pre-order Traversal
Вот алгоритм **pre-order traversal**:
1. Проверьте, является ли текущий узел пустым/нулевым.
2. Отобразите часть данных корня (или текущего узла).
3. Пройдите по левому поддереву, рекурсивно вызывая метод preorder.
4. Пройдите по правому поддереву, рекурсивно вызывая метод preorder.

        def preorder_print(self, start, traversal):
            """Root->Left->Right"""
            if start:
                traversal += (str(start.value) + "-")
                traversal = self.preorder_print(start.left, traversal)
                traversal = self.preorder_print(start.right, traversal)
            return traversal
            
## 2. In-order Traversal
Вот алгоритм in-order traversal:
1. Проверьте, является ли текущий узел пустым/нулевым.
2. Пройдите по левому поддереву, рекурсивно вызывая метод упорядочения.
3. Отобразите часть данных корня (или текущего узла).
4. Пройдите по правому поддереву, рекурсивно вызывая метод упорядочения.

        def inorder_print(self, start, traversal):
            """Left->Root->Right"""
            if start:
                traversal = self.inorder_print(start.left, traversal)
                traversal += (str(start.value) + "-")
                traversal = self.inorder_print(start.right, traversal)
            return traversal
            
## 3. Post-order Traversal

Aлгоритм Post-order Traversal:

1. Проверьте, является ли текущий узел пустым / нулевым.
2. Пройдите по левому поддереву, рекурсивно вызывая метод пост-заказа.
3. Пройдите по правому поддереву, рекурсивно вызывая метод пост-заказа.
4. Отобразите часть данных корня (или текущего узла).

        def postorder_print(self, start, traversal):
            """Left->Right->Root"""
            if start:
                traversal = self.postorder_print(start.left, traversal)
                traversal = self.postorder_print(start.right, traversal)
                traversal += (str(start.value) + "-")
            return traversal
            
## Level-Order Traversal

Во-первых, нам нужно реализовать Queue, чтобы мы могли использовать его объект в нашем решении обхода порядка уровней.

        class Queue(object):
            def __init__(self):
                self.items = []

            def enqueue(self, item):
                self.items.insert(0, item)

            def dequeue(self):
                if not self.is_empty():
                    return self.items.pop()

            def is_empty(self):
                return len(self.items) == 0

            def peek(self):
                if not self.is_empty():
                    return self.items[-1].value

            def __len__(self):
                return self.size()

            def size(self):
                return len(self.items)
                
Теперь, когда мы успешно реализовали Queueкласс, давайте продолжим и реализуем обход в порядке уровней:
    
        def levelorder_print(self, start):
            if start is None:
                return 

            queue = Queue()
            queue.enqueue(start)

            traversal = ""
            while len(queue) > 0:
                traversal += str(queue.peek()) + "-"
                node = queue.dequeue()

            if node.left:
                queue.enqueue(node.left)
            if node.right:
                queue.enqueue(node.right)

            return traversal
         
