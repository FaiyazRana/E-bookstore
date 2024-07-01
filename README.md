# Database design for E-bookstore

## Duties and responsibilities

- *Database Design:*  Faiyaz is taking care  for creating the database schema, including tables, relationships, and constraints.
- *Data Insertion:* Abrar is handling and taking care  for inserting sample data into the database tables.
- *Query Writing:* Naveed is taking care for  writing SQL queries to fulfill the bookstore's requirements.
- *TypeScript Interface:* Faiyaz and abrar both  handling and taking care for creating a TypeScript interface for table modification.

**SQL queries, table creation, DDL, DML And typescript with CRUD Operation.**



```sql 
-- Create table for authors
CREATE TABLE authors (
    authorid SERIAL PRIMARY KEY,
    name VARCHAR(100)
);

-- Create table for genres
CREATE TABLE genres (
    genre_id SERIAL PRIMARY KEY,
    name VARCHAR(50)
);

-- Create table for books
CREATE TABLE books (
    book_id SERIAL PRIMARY KEY,
    title VARCHAR(200),
    genre_id INT,
    author_id INT,
    publisher_id INT,
    published_date DATE,
    rating DECIMAL(3, 2),
    FOREIGN KEY (genre_id) REFERENCES genres(genre_id),
    FOREIGN KEY (author_id) REFERENCES authors(authorid)
);

-- Create table for publishers
CREATE TABLE publishers (
    publisher_id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);

-- Create table for customers
CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    join_date DATE,
    total_spent DECIMAL(10, 2)
);

-- Create table for reviews
CREATE TABLE reviews (
    review_id SERIAL PRIMARY KEY,
    book_id INT,
    customer_id INT,
    review_date DATE,
    rating DECIMAL(3, 2),
    comment TEXT,
    FOREIGN KEY (book_id) REFERENCES books(book_id),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

-- Create table for sales
CREATE TABLE sales (
    sale_id SERIAL PRIMARY KEY,
    book_id INT,
    customer_id INT,
    sale_date DATE,
    amount DECIMAL(10, 2),
    FOREIGN KEY (book_id) REFERENCES books(book_id),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

-- Insert data into authors table
INSERT INTO authors (name) VALUES 
('Alice Walker'), 
('George Orwell'), 
('Agatha Christie'), 
('J.K. Rowling'), 
('Ernest Hemingway'), 
('Toni Morrison'), 
('James Patterson'), 
('Stephen King'), 
('F. Scott Fitzgerald'), 
('Harper Lee');

-- Insert data into genres table
INSERT INTO genres (name) VALUES 
('Drama'), 
('Thriller'), 
('Romance'),
('Mystery'), 
('Science Fiction'), 
('Fantasy'), 
('Biography'), 
('Non-Fiction'), 
('Historical Fiction'), 
('Horror');

-- Insert data into books table
INSERT INTO books (title, genre_id, author_id, publisher_id, published_date, rating) VALUES 
('The Color Purple', 1, 1, 1, '1982-09-17', 4.9), 
('1984', 5, 2, 2, '1949-06-08', 4.7), 
('Murder on the Orient Express', 4, 3, 3, '1934-01-01', 4.6), 
('Harry Potter and the Philosopher', 6, 4, 4, '1997-06-26', 4.8), 
('The Old Man and the Sea', 9, 5, 5, '1952-09-01', 4.5), 
('Beloved', 1, 6, 6, '1987-09-16', 4.9), 
('Along Came a Spider', 2, 7, 7, '1993-01-01', 4.2), 
('The Shining', 10, 8, 8, '1977-01-28', 4.8), 
('The Great Gatsby', 9, 9, 9, '1925-04-10', 4.4), 
('To Kill a Mockingbird', 1, 10, 10, '1960-07-11', 4.9);

-- Insert data into publishers table
INSERT INTO publishers (name) VALUES 
('Penguin Random House'), 
('HarperCollins'), 
('Macmillan Publishers'), 
('Bloomsbury'), 
('Scribner'), 
('Knopf'), 
('Little, Brown and Company'), 
('Doubleday'), 
('Charles Scribners Sons'), 
('J.B. Lippincott & Co.');

-- Insert data into customers table
INSERT INTO customers (name, email, join_date, total_spent) VALUES 
('Faiyaz rana', 'faiyaz@gmai.com.com', '2023-01-15', 150.50), 
('abrar malek', 'abrar@gmail.com', '2022-03-22', 220.75), 
('naveed khan', 'naveed@gmail.com', '2024-05-15', 320.00), 
('Emily Davis', 'emily.davis@gmail.com', '2024-06-25', 180.00), 
('Michael Wilson', 'michael.wilson@gmail.com', '2023-04-12', 240.00), 
('Sarah Johnson', 'sarah.johnson@gmail.com', '2023-07-08', 400.00), 
('David Moore', 'david.moore@gamil.com', '2023-08-14', 310.50), 
('Laura Taylor', 'laura.taylor@gmail.com', '2023-09-20', 150.00), 
('James Anderson', 'james.anderson@gmail.com', '2024-04-01', 250.75), 
('Linda Martinez', 'linda.martinez@gmail.com', '2023-11-15', 300.00);

-- Insert data into reviews table
INSERT INTO reviews (book_id, customer_id, review_date, rating, comment) VALUES 
(1, 1, '2023-02-01', 4.5, 'Incredible story and characters.'), 
(2, 2, '2023-04-05', 4.7, 'A thought-provoking dystopian novel.'), 
(3, 3, '2024-06-18', 4.6, 'A classic mystery that never gets old.'), 
(4, 4, '2024-06-27', 5.0, 'A magical journey from start to finish.'), 
(5, 5, '2023-05-02', 4.3, 'A beautifully written novella.'), 
(6, 6, '2023-08-01', 4.9, 'A haunting and powerful narrative.'), 
(7, 7, '2023-09-01', 4.2, 'A gripping thriller with great twists.'), 
(8, 8, '2023-10-10', 4.8, 'A chilling horror story.'), 
(9, 9, '2024-05-20', 4.4, 'A timeless classic.'), 
(10, 10, '2023-12-15', 4.9, 'A must-read novel for all ages.');

-- Insert data into sales table
INSERT INTO sales (book_id, customer_id, sale_date, amount) VALUES 
(1, 1, '2023-01-20', 20.99), 
(2, 2, '2023-04-10', 15.99), 
(3, 3, '2024-05-20', 12.99), 
(4, 4, '2024-06-30', 18.99), 
(5, 5, '2023-04-20', 10.99), 
(6, 6, '2023-07-15', 22.99), 
(7, 7, '2023-08-20', 17.99), 
(8, 8, '2023-09-25', 25.99), 
(9, 9, '2024-04-15', 14.99), 
(10, 10, '2023-11-20', 19.99);

--Power writers (authors) with more than X books in the same genre published within the last X years --
SELECT 
    A.name AS AuthorName, 
    G.name AS Genre, 
    COUNT(B.book_id) AS TotalBooks
FROM 
    authors A
JOIN 
    books B ON A.authorid = B.author_id
JOIN 
    genres G ON B.genre_id = G.genre_id
WHERE 
    B.published_date >= CURRENT_DATE - INTERVAL '3 years'
GROUP BY 
    A.name, G.name
HAVING 
    COUNT(B.book_id) > 2;


--Loyal Customers who has spent more than X dollars in the last year--

SELECT 
    name AS CustomerName, 
    email AS Email, 
    join_date AS JoinDate, 
    total_spent AS TotalSpent
FROM 
    customers
WHERE 
    total_spent > 300
AND 
    join_date >= CURRENT_DATE - INTERVAL '1 year';


--Well Reviewed books that has a better user rating than average

SELECT 
    B.title AS BookTitle, 
    AVG(R.rating) AS AvgRating
FROM 
    books B
JOIN 
    reviews R ON B.book_id = R.book_id
GROUP BY 
    B.title
HAVING 
    AVG(R.rating) > (SELECT AVG(rating) FROM reviews);

---The most popular genre by sales--

SELECT 
    G.name AS Genre, 
    SUM(S.amount) AS TotalSales
FROM 
    genres G
JOIN 
    books B ON G.genre_id = B.genre_id
JOIN 
    sales S ON B.book_id = S.book_id
GROUP BY 
    G.name
ORDER BY 
    TotalSales DESC
LIMIT 1;


--The 10 most recent posted reviews by Customers 
--
SELECT 
    R.review_id AS ReviewID, 
    B.title AS BookTitle, 
    C.name AS CustomerName, 
    R.review_date AS ReviewDate, 
    R.rating AS Rating, 
    R.comment AS Comment
FROM 
    reviews R
JOIN 
    books B ON R.book_id = B.book_id
JOIN 
    customers C ON R.customer_id = C.customer_id
ORDER BY 
    R.review_date DESC
LIMIT 10;



DDL (Data Definition Language)
-- Create table for books
CREATE TABLE books (
    book_id SERIAL PRIMARY KEY,
    title VARCHAR(200),
    genre_id INT,
    author_id INT,
    publisher_id INT,
    published_date DATE,
    rating DECIMAL(3, 2),
    FOREIGN KEY (genre_id) REFERENCES genres(genre_id),
    FOREIGN KEY (author_id) REFERENCES authors(authorid)

);


DML(Data Manipulation Language)
--insert data into books table

INSERT INTO books (title, genre_id, author_id, publisher_id, published_date, rating) VALUES 
('The Color Purple', 1, 1, 1, '1982-09-17', 4.9), 
('1984', 5, 2, 2, '1949-06-08', 4.7), 
('Murder on the Orient Express', 4, 3, 3, '1934-01-01', 4.6), 
('Harry Potter and the Philosopher', 6, 4, 4, '1997-06-26', 4.8), 
('The Old Man and the Sea', 9, 5, 5, '1952-09-01', 4.5), 
('Beloved', 1, 6, 6, '1987-09-16', 4.9), 
('Along Came a Spider', 2, 7, 7, '1993-01-01', 4.2), 
('The Shining', 10, 8, 8, '1977-01-28', 4.8), 
('The Great Gatsby', 9, 9, 9, '1925-04-10', 4.4), 
('To Kill a Mockingbird', 1, 10, 10, '1960-07-11', 4.9);



--TYPESCRIPT  and CRUD OPERATION --
// Import necessary modules
import { Pool } from 'pg';

// Define interfaces for database entities
interface Author {
    author_id?: number; 
    name: string;
}

interface Genre {
    genre_id?: number; 
    name: string;
}

interface Book {
    book_id?: number; 
    title: string;
    genre_id: number;
    author_id: number;
    publisher_id: number;
    published_date: Date;
    rating: number;
}

interface Publisher {
    publisher_id?: number; 
    name: string;
}

interface Customer {
    customer_id?: number; 
    name: string;
    email: string;
    join_date: Date;
    total_spent: number;
}

interface Review {
    review_id?: number; 
    book_id: number;
    customer_id: number;
    review_date: Date;
    rating: number;
    comment: string;
}

interface Sale {
    sale_id?: number; 
    book_id: number;
    customer_id: number;
    sale_date: Date;
    amount: number;
}

// Database connection configuration
const pool = new Pool({
    user: 'Postgres',
    host: 'localhost',
    database: 'bookstore',
    password: 'password',
    port: 5432, // or your PostgreSQL port
});

// Function to handle database queries
async function query(text: string, params?: any[]) {
    const client = await pool.connect();
    try {
        const result = await client.query(text, params);
        return result;
    } finally {
        client.release();
    }
}

// CRUD operations for Authors
async function createAuthor(author: Author): Promise<Author | null> {
    const { name } = author;
    const queryText = 'INSERT INTO authors (name) VALUES ($1) RETURNING *';
    const values = [name];
    const result = await query(queryText, values);
    return result.rows[0] as Author;
}

async function getAuthors(): Promise<Author[]> {
    const queryText = 'SELECT * FROM authors';
    const result = await query(queryText);
    return result.rows as Author[];
}

async function updateAuthor(authorId: number, name: string): Promise<Author | null> {
    const queryText = 'UPDATE authors SET name = $1 WHERE author_id = $2 RETURNING *';
    const values = [name, authorId];
    const result = await query(queryText, values);
    return result.rows[0] as Author;
}

async function deleteAuthor(authorId: number): Promise<boolean> {
    const queryText = 'DELETE FROM authors WHERE author_id = $1';
    const values = [authorId];
    const result = await query(queryText, values);
    return result.rowCount > 0;
}

// CRUD operations for Genres
async function createGenre(genre: Genre): Promise<Genre | null> {
    const { name } = genre;
    const queryText = 'INSERT INTO genres (name) VALUES ($1) RETURNING *';
    const values = [name];
    const result = await query(queryText, values);
    return result.rows[0] as Genre;
}

async function getGenres(): Promise<Genre[]> {
    const queryText = 'SELECT * FROM genres';
    const result = await query(queryText);
    return result.rows as Genre[];
}

// CRUD operations for Books
async function createBook(book: Book): Promise<Book | null> {
    const { title, genre_id, author_id, publisher_id, published_date, rating } = book;
    const queryText = 'INSERT INTO books (title, genre_id, author_id, publisher_id, published_date, rating) VALUES ($1, $2, $3, $4, $5, $6) RETURNING *';
    const values = [title, genre_id, author_id, publisher_id, published_date, rating];
    const result = await query(queryText, values);
    return result.rows[0] as Book;
}

async function getBooks(): Promise<Book[]> {
    const queryText = 'SELECT * FROM books';
    const result = await query(queryText);
    return result.rows as Book[];
}

// CRUD operations for Publishers
async function createPublisher(publisher: Publisher): Promise<Publisher | null> {
    const { name } = publisher;
    const queryText = 'INSERT INTO publishers (name) VALUES ($1) RETURNING *';
    const values = [name];
    const result = await query(queryText, values);
    return result.rows[0] as Publisher;
}

async function getPublishers(): Promise<Publisher[]> {
    const queryText = 'SELECT * FROM publishers';
    const result = await query(queryText);
    return result.rows as Publisher[];
}

// CRUD operations for Customers
async function createCustomer(customer: Customer): Promise<Customer | null> {
    const { name, email, join_date, total_spent } = customer;
    const queryText = 'INSERT INTO customers (name, email, join_date, total_spent) VALUES ($1, $2, $3, $4) RETURNING *';
    const values = [name, email, join_date, total_spent];
    const result = await query(queryText, values);
    return result.rows[0] as Customer;
}

async function getCustomers(): Promise<Customer[]> {
    const queryText = 'SELECT * FROM customers';
    const result = await query(queryText);
    return result.rows as Customer[];
}

// CRUD operations for Reviews
async function createReview(review: Review): Promise<Review | null> {
    const { book_id, customer_id, review_date, rating, comment } = review;
    const queryText = 'INSERT INTO reviews (book_id, customer_id, review_date, rating, comment) VALUES ($1, $2, $3, $4, $5) RETURNING *';
    const values = [book_id, customer_id, review_date, rating, comment];
    const result = await query(queryText, values);
    return result.rows[0] as Review;
}

async function getReviews(): Promise<Review[]> {
    const queryText = 'SELECT * FROM reviews';
    const result = await query(queryText);
    return result.rows as Review[];
}

// CRUD operations for Sales
async function createSale(sale: Sale): Promise<Sale | null> {
    const { book_id, customer_id, sale_date, amount } = sale;
    const queryText = 'INSERT INTO sales (book_id, customer_id, sale_date, amount) VALUES ($1, $2, $3, $4) RETURNING *';
    const values = [book_id, customer_id, sale_date, amount];
    const result = await query(queryText, values);
    return result.rows[0] as Sale;
}

async function getSales(): Promise<Sale[]> {
    const queryText = 'SELECT * FROM sales';
    const result = await query(queryText);
    return result.rows as Sale[];
}

// Example usage:
async function main() {
    try {
        // Begin a transaction
        await pool.query('BEGIN');

        // Example: Create a new author
        const newAuthor: Author = { name: 'Jane Austen' };
        const createdAuthor = await createAuthor(newAuthor);
        console.log('Created author:', createdAuthor);

        // Example: Get all authors
        const authors = await getAuthors();
        console.log('All authors:', authors);

        // Example: Update an author
        if (authors.length > 0) {
            const updatedAuthor = await updateAuthor(authors[0].author_id!, 'Jane Austen (Updated)');
            console.log('Updated author:', updatedAuthor);
        }

        // Example: Delete an author
        if (authors.length > 1) {
            const deleted = await deleteAuthor(authors[1].author_id!);
            console.log('Author deleted successfully:', deleted);
        }

        // Commit the transaction
        await pool.query('COMMIT');
    } catch (e) {
        // Rollback the transaction in case of error
        await pool.query('ROLLBACK');
        console.error('Error in transaction:', e);
    } finally {
        // End the pool connection
        await pool.end();
    }
}

main();


```
