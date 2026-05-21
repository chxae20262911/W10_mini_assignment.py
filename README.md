# W10_mini_assignment.py
class EBook(Book):
    def __init__(self, title, author, pages, file_size):
        if file_size < 0:
            raise ValueError("file_size는 0 이상이어야 합니다.")
        super().__init__(title, author, pages)
        self.file_size = file_size

    def __str__(self):
        return f"[eBook] {self.title} by {self.author} ({self.pages}p, {self.file_size}MB)"

    def reading_time(self, wpm=250):
        return self.pages * 250 // wpm


class AudioBook(Book):
    def __init__(self, title, author, pages, duration):
        if duration < 0:
            raise ValueError("duration은 0 이상이어야 합니다.")
        super().__init__(title, author, pages)
        self.duration = duration

    def __str__(self):
        hour = self.duration // 60
        minute = self.duration % 60
        return f"[오디오북] {self.title} by {self.author} ({self.pages}p, {hour}h {minute}m)"

    def reading_time(self):
        return self.duration


def print_book_info(book):
    print(book)


def main():
    library = [
        Book("어린왕자", "생텍쥐페리", 96),
        EBook("파이썬 입문", "점프 투 파이썬", 300, 2.4),
        AudioBook("해리포터", "롤링", 223, 135),
        EBook("코스모스", "칼 세이건", 365, 5.1),
        AudioBook("사피엔스", "유발 하라리", 638, 312),
    ]

    print("=" * 40)
    print("📚 전체 도서 목록")
    print("=" * 40)

    for book in library:
        print_book_info(book)

    print()
    print("=" * 40)
    print("📖 페이지 수 기준 정렬")
    print("=" * 40)

    sorted_library = sorted(library)

    for book in sorted_library:
        print_book_info(book)

    print()
    print("=" * 40)
    print("📊 종류별 통계")
    print("=" * 40)

    normal_count = 0
    ebook_count = 0
    audiobook_count = 0

    for book in library:
        if isinstance(book, AudioBook):
            audiobook_count += 1
        elif isinstance(book, EBook):
            ebook_count += 1
        elif isinstance(book, Book):
            normal_count += 1

    print(f"일반 도서: {normal_count}권  /  전자책: {ebook_count}권  /  오디오북: {audiobook_count}권")

    print()
    print("=" * 40)
    print("⏱ 예상 독서 시간")
    print("=" * 40)

    for book in library:
        print(f"{book.title}: {book.reading_time()}분")


if __name__ == "__main__":
    main()
