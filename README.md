# Библиотека выдачи книг
class Book:
    def __init__(self, title, author, isbn):
        self.title = title
        self.author = author
        self.isbn = isbn
        self.available = True

    def __str__(self):
        return f"{self.title} by {self.author} (ISBN: {self.isbn})"

class Patron:
    def __init__(self, name, library_card):
        self.name = name
        self.library_card = library_card
        self.checked_out_books = []

    def checkout_book(self, book):
        if book.available:
            book.available = False
            self.checked_out_books.append(book)
            return f"Вы успешно взяли '{book.title}'"
        return "К сожалению, книга в данный момент недоступна"

    def return_book(self, book):
        if book in self.checked_out_books:
            book.available = True
            self.checked_out_books.remove(book)
            return f"Книга '{book.title}' успешно возвращена"
        return "Такая книга не найдена в вашем списке"

class Library:
    def __init__(self):
        self.books = []
        self.patrons = []

    def add_book(self, book):
        self.books.append(book)

    def add_patron(self, patron):
        self.patrons.append(patron)

    def search_book(self, title):
        return [book for book in self.books if title.lower() in book.title.lower()]

# Пример использования
if __name__ == "__main__":
    # Создаем библиотеку
    library = Library()

    # Добавляем книги
    book1 = Book("Война и мир", "Лев Толстой", "978-5-0000-0000-1")
    book2 = Book("1984", "Джордж Оруэлл", "978-5-0000-0000-2")
    library.add_book(book1)
    library.add_book(book2)

    # Добавляем читателя
    patron = Patron("Иван Петров", "A12345")
    library.add_patron(patron)

    # Выдача книги
    print(patron.checkout_book(book1))
    
    # Поиск книг
    search_results = library.search_book("война")
    for book in search_results:
        print(book)

    # Возврат книги
    print(patron.return_book(book1))
    
