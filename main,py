# Класс узла графа
class Vertex:
    def __init__(self, key):
        self.key = key  # Имя вершины
        self.edges = {}  # Рёбра {имя второй вершины:вес}

    def __str__(self):  # Вывод вершины и её рёбер
        return str(self.key)+str(self.edges)


# Класс графа
class Graph:

    def __init__(self):
        self.all_vertex = []  # Все вершины графа

    def add_vertex(self, key):  # Добавление вершины
        self.all_vertex.append(Vertex(key))

    def add_edge(self, key1, key2, weight):  # Добавляет в vertex1.edges key2 а в vertex2.edges.key1 с весами
        for vertex in self.all_vertex:
            if vertex.key == key1:
                vertex.edges[key2] = weight
            if vertex.key == key2:
                vertex.edges[key1] = weight

    def __str__(self):  # Вывод графа
        output = ''
        for i in range(len(self.all_vertex)):
            v = self.all_vertex[i]
            end = ', ' if i < len(self.all_vertex) - 1 else ''
            output += str(v)+end
        return output

    def get_vertex(self, key):  # Получаем вершину с рёбрами по её имени
        for vertex in self.all_vertex:
            if vertex.key == key:
                return vertex

    def max_path(self):  # Сумма всех весов +1: самый длинный возможный путь
        output = 1
        for vertex in self.all_vertex:
            output += sum(vertex.edges.values())
        return output

    def dijkstra(self, start, end):  # Поиск кратчайшего пути от start до end, отдаёт длину и маршрут
        lenghts = {}  # Веса всех вершин {имя: вес}
        current_vertex = self.get_vertex(start)  # Начальная точка
        path = {}  # Кратчайшие маршруты от start до всех вершин
        inf = self.max_path()
        for vertex in self.all_vertex:
            path[vertex.key] = start  # Начальная точка любого маршрута
            lenghts[vertex.key] = 0 if vertex.key == start else inf  # У всех вершин максимальный вес, кроме start
        unseen = lenghts.copy()  # Список ещё непосещённых вершин
        while unseen:
            for i, j in current_vertex.edges.items():
                lenghts[i] = j + lenghts[current_vertex.key] if i in unseen else lenghts[i]  # Warning, but work :)
                if i in unseen:
                    path[i] = path.get(current_vertex.key)+i
                if unseen.get(i):
                    unseen[i] = lenghts[i]
            unseen.pop(current_vertex.key)
            if unseen:  # FIXME: где-то лажа
                current_vertex = self.get_vertex(min(unseen, key=lambda k: unseen[k]))  # Чёрная магия
        if lenghts[end] == inf:  # Если пути не найдено, то исключение
            raise Exception('Нет пути!')
        return lenghts[end], path[end]



# #### ПРИМЕРЫ ### #
mygraph = Graph()  # Создаём граф
mygraph.add_vertex('Z')  # Добавляем вершины
mygraph.add_vertex('A')
mygraph.add_vertex('B')
mygraph.add_vertex('C')
mygraph.add_vertex('D')
mygraph.add_edge('A', 'C', 3)  # Соединяем вершины рёбрами
mygraph.add_edge('A', 'B', 15)
mygraph.add_edge('B', 'C', 5)
mygraph.add_edge('C', 'D', 2)
mygraph.add_edge('Z', 'A', 1)
print(mygraph)  # Выводим граф
print(mygraph.dijkstra('Z', 'D'))  # Выводим длину кратчайшего пути и маршрут кратчайшего пути
