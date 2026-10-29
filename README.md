# PHINMA-COC-STUDENT-LIBRARY-BORROWING-SYSTEM
[library_db (4).sql](https://github.com/user-attachments/files/34112207/library_db.4.sql)
-- phpMyAdmin SQL Dump
-- version 5.2.1
-- https://www.phpmyadmin.net/
--
-- Host: 127.0.0.1
-- Generation Time: Oct 13, 2026 at 06:55 AM
-- Server version: 10.4.32-MariaDB
-- PHP Version: 8.2.12

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Database: `library_db`
--

-- --------------------------------------------------------

--
-- Table structure for table `books`
--

CREATE TABLE `books` (
  `book_id` int(11) NOT NULL,
  `title` varchar(200) NOT NULL,
  `author` varchar(150) NOT NULL,
  `category_id` int(11) DEFAULT NULL,
  `isbn` varchar(30) DEFAULT NULL,
  `quantity` int(11) NOT NULL DEFAULT 0,
  `available_copies` int(11) NOT NULL DEFAULT 0,
  `is_archived` tinyint(1) NOT NULL DEFAULT 0
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `books`
--

INSERT INTO `books` (`book_id`, `title`, `author`, `category_id`, `isbn`, `quantity`, `available_copies`, `is_archived`) VALUES
(1, 'Java Programming', 'James Smith', 1, '9780000000011', 5, 5, 1),
(2, 'Database Systems', 'John Doe', 2, '9780000000028', 89, 89, 0),
(3, 'ivy', 'angel', 5, '6583916425789', 1, 1, 0),
(4, 'ghj', 'hjk', 6, '7895461034763', 5, 5, 0),
(5, 'dragon', 'wenz', 7, '1234567890123', 5, 5, 0),
(6, 'programming', 'Project', 24, '2345534253223', 10, 10, 1),
(7, 'Human Behaviour', 'Beth Zaragosa', 3, '2254615879456', 1, 1, 0),
(8, 'Medical Physiology', 'Beth Zaragosa', 8, '8736456278364', 5, 5, 0),
(9, 'Java Programming', 'Reene Casicas', 1, '5454562154123', 10, 10, 0),
(10, 'dragons', 'angel', 5, '1234567890753', 5, 5, 0),
(11, 'Human Computer Interaction', 'Angel Mae Mutia', 2, '1267637663738', 10, 10, 0),
(12, 'Introduction to Computing', 'Berna Pabua', 2, '4526637383892', 10, 10, 0),
(13, 'Java', 'Renee Casicas', 2, '1234567890987', 99, 99, 0),
(14, 'hook', 'ako', 29, '8766789876899', 1, 1, 0),
(15, 'tangled', 'irish wenz', 9, '1212345678900', 10, 10, 0);

-- --------------------------------------------------------

--
-- Table structure for table `borrow_items`
--

CREATE TABLE `borrow_items` (
  `borrow_items_id` int(11) NOT NULL,
  `transaction_id` int(11) NOT NULL,
  `book_id` int(11) NOT NULL,
  `return_date` date DEFAULT NULL,
  `status` enum('Borrowed','Returned') NOT NULL DEFAULT 'Borrowed',
  `quantity` int(11) NOT NULL DEFAULT 1
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `borrow_items`
--

INSERT INTO `borrow_items` (`borrow_items_id`, `transaction_id`, `book_id`, `return_date`, `status`, `quantity`) VALUES
(1, 13, 7, '2026-10-06', 'Returned', 1),
(2, 13, 8, '2026-10-06', 'Returned', 1),
(3, 13, 9, '2026-10-06', 'Returned', 1),
(4, 14, 2, '2026-10-07', 'Returned', 3),
(5, 15, 9, '2026-10-07', 'Returned', 2),
(6, 16, 8, '2026-10-12', 'Returned', 1),
(7, 17, 2, '2026-10-12', 'Returned', 1),
(8, 17, 1, '2026-10-12', 'Returned', 1),
(9, 18, 2, '2026-10-12', 'Returned', 1),
(10, 18, 7, '2026-10-12', 'Returned', 1),
(11, 19, 2, '2026-10-12', 'Returned', 1),
(12, 20, 2, '2026-10-12', 'Returned', 88),
(13, 20, 7, '2026-10-12', 'Returned', 1),
(14, 20, 11, '2026-10-12', 'Returned', 1),
(15, 20, 1, '2026-10-12', 'Returned', 5),
(16, 20, 8, '2026-10-12', 'Returned', 1),
(17, 21, 2, '2026-10-12', 'Returned', 89),
(18, 21, 8, '2026-10-12', 'Returned', 5),
(19, 21, 10, '2026-10-12', 'Returned', 5),
(20, 21, 4, '2026-10-12', 'Returned', 5),
(21, 21, 7, '2026-10-12', 'Returned', 1),
(22, 21, 11, '2026-10-12', 'Returned', 10),
(23, 21, 5, '2026-10-12', 'Returned', 5);

-- --------------------------------------------------------

--
-- Table structure for table `borrow_transactions`
--

CREATE TABLE `borrow_transactions` (
  `transaction_id` int(11) NOT NULL,
  `student_id` int(11) NOT NULL,
  `processed_by` int(11) DEFAULT NULL,
  `borrow_date` date NOT NULL,
  `due_date` date NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `borrow_transactions`
--

INSERT INTO `borrow_transactions` (`transaction_id`, `student_id`, `processed_by`, `borrow_date`, `due_date`) VALUES
(13, 7, 1, '2026-10-06', '2026-10-13'),
(14, 1, 1, '2026-10-07', '2026-10-14'),
(15, 4, 1, '2026-10-07', '2026-10-14'),
(16, 1, 1, '2026-10-08', '2026-10-15'),
(17, 3, 1, '2026-10-11', '2026-10-25'),
(18, 9, 1, '2026-10-12', '2026-11-02'),
(19, 7, 1, '2026-10-12', '2026-10-19'),
(20, 7, 1, '2026-10-12', '2026-10-19'),
(21, 14, 1, '2026-10-12', '2026-10-26');

-- --------------------------------------------------------

--
-- Table structure for table `categories`
--

CREATE TABLE `categories` (
  `category_id` int(11) NOT NULL,
  `category_name` varchar(100) NOT NULL,
  `is_archived` tinyint(1) NOT NULL DEFAULT 0
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `categories`
--

INSERT INTO `categories` (`category_id`, `category_name`, `is_archived`) VALUES
(1, 'Programming', 0),
(2, 'IT', 0),
(3, 'Science', 0),
(4, 'General', 0),
(5, 'bsed', 1),
(6, 'vbn', 1),
(7, 'horror', 0),
(8, 'Science and Health', 0),
(9, 'Fiction', 0),
(10, 'Non-Fiction', 0),
(11, 'Reference', 0),
(12, 'Textbooks', 0),
(13, 'General Works', 0),
(14, 'Philosophy and Psychology', 0),
(15, 'Religion', 0),
(16, 'Social Sciences', 0),
(17, 'Language and Linguistics', 0),
(18, 'Natural Sciences', 0),
(19, 'Mathematics', 0),
(20, 'Computer Science and IT', 0),
(21, 'Technology and Engineering', 0),
(22, 'Health and Medicine', 0),
(23, 'Arts and Recreation', 0),
(24, 'Literature', 0),
(25, 'History and Geography', 0),
(26, 'Filipino', 0),
(27, 'English', 0),
(28, 'Biology', 0),
(29, 'Chemistry', 0),
(30, 'Physics', 0),
(31, 'Earth and Space Science', 0),
(32, 'Social Studies', 0),
(33, 'Values Education', 0),
(34, 'Dictionaries and Encyclopedias', 0),
(35, 'Research and Theses', 0),
(36, 'Children\'s Books', 0),
(37, 'Periodicals and Magazines', 0),
(38, 'Prolaloy', 0);

-- --------------------------------------------------------

--
-- Table structure for table `departments`
--

CREATE TABLE `departments` (
  `department_id` int(11) NOT NULL,
  `department_name` varchar(100) NOT NULL,
  `is_archived` tinyint(1) NOT NULL DEFAULT 0
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `departments`
--

INSERT INTO `departments` (`department_id`, `department_name`, `is_archived`) VALUES
(1, 'CITE', 0),
(2, 'CMA', 0),
(3, 'CEA', 0),
(4, 'SCCJ', 0),
(5, 'CAHS', 0),
(8, 'BBM', 1);

-- --------------------------------------------------------

--
-- Table structure for table `students`
--

CREATE TABLE `students` (
  `student_id` int(11) NOT NULL,
  `school_id` varchar(30) NOT NULL,
  `first_name` varchar(75) NOT NULL,
  `last_name` varchar(75) NOT NULL,
  `department_id` int(11) NOT NULL,
  `year_level_id` int(11) NOT NULL,
  `contact` varchar(30) DEFAULT NULL,
  `is_archived` tinyint(1) NOT NULL DEFAULT 0
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `students`
--

INSERT INTO `students` (`student_id`, `school_id`, `first_name`, `last_name`, `department_id`, `year_level_id`, `contact`, `is_archived`) VALUES
(1, '02-2526-013235', 'mcmiel', 'ganora', 1, 2, '12384845412', 1),
(2, '02-2526-013803', 'wenz', 'borja', 1, 5, '09058884262', 1),
(3, '02414', 'julooo', 'Ganora', 1, 2, '27364923647', 0),
(4, '0262519273', 'eunice', 'butoy', 1, 2, '12368412346', 1),
(5, '23', 'bag', 'as', 1, 6, '032098552', 1),
(6, '2526', 'lovelle', 'oclarit', 1, 7, '0929963728', 1),
(7, '2526-030802', 'Angel Mae', 'Mutia', 2, 8, '25461254612', 0),
(8, '2526-030803', 'Mcmiel', 'Ganora', 1, 5, '51245876452', 1),
(9, '2526-030804', 'Lovelle', 'Oclarit', 1, 2, '76754356768', 0),
(10, '333', 'wenz', 'ambt', 3, 7, '090111111', 1),
(12, '022526013425', 'ian', 'arranchado', 2, 3, '09126431524', 1),
(14, '2526-021656', 'Cherrylin', 'Borja', 1, 4, '09763736478', 0),
(15, '02-1222-212123', 'Wenz', 'Borja', 3, 3, '09058884262', 0);

-- --------------------------------------------------------

--
-- Table structure for table `users`
--

CREATE TABLE `users` (
  `user_id` int(11) NOT NULL,
  `username` varchar(50) NOT NULL,
  `password` varchar(255) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `users`
--

INSERT INTO `users` (`user_id`, `username`, `password`) VALUES
(1, 'admin', 'admin123');

-- --------------------------------------------------------

--
-- Table structure for table `year_levels`
--

CREATE TABLE `year_levels` (
  `year_level_id` int(11) NOT NULL,
  `year_level_name` varchar(100) NOT NULL,
  `is_archived` tinyint(1) NOT NULL DEFAULT 0
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

--
-- Dumping data for table `year_levels`
--

INSERT INTO `year_levels` (`year_level_id`, `year_level_name`, `is_archived`) VALUES
(1, '1 year', 0),
(2, '2 year', 0),
(3, '3 year', 0),
(4, '4 year', 0),
(5, '3rdyear', 1),
(6, '4th', 1),
(7, '2nd Year', 1),
(8, '2nd', 1);

--
-- Indexes for dumped tables
--

--
-- Indexes for table `books`
--
ALTER TABLE `books`
  ADD PRIMARY KEY (`book_id`),
  ADD KEY `fk_book_category` (`category_id`);

--
-- Indexes for table `borrow_items`
--
ALTER TABLE `borrow_items`
  ADD PRIMARY KEY (`borrow_items_id`),
  ADD UNIQUE KEY `uq_borrow_items_transaction_book` (`transaction_id`,`book_id`),
  ADD KEY `fk_item_book` (`book_id`);

--
-- Indexes for table `borrow_transactions`
--
ALTER TABLE `borrow_transactions`
  ADD PRIMARY KEY (`transaction_id`),
  ADD KEY `fk_transaction_student` (`student_id`),
  ADD KEY `fk_transaction_user` (`processed_by`);

--
-- Indexes for table `categories`
--
ALTER TABLE `categories`
  ADD PRIMARY KEY (`category_id`),
  ADD UNIQUE KEY `category_name` (`category_name`);

--
-- Indexes for table `departments`
--
ALTER TABLE `departments`
  ADD PRIMARY KEY (`department_id`),
  ADD UNIQUE KEY `department_name` (`department_name`);

--
-- Indexes for table `students`
--
ALTER TABLE `students`
  ADD PRIMARY KEY (`student_id`),
  ADD UNIQUE KEY `uq_students_school_id` (`school_id`),
  ADD KEY `fk_student_department` (`department_id`),
  ADD KEY `fk_student_year_level` (`year_level_id`);

--
-- Indexes for table `users`
--
ALTER TABLE `users`
  ADD PRIMARY KEY (`user_id`),
  ADD UNIQUE KEY `username` (`username`);

--
-- Indexes for table `year_levels`
--
ALTER TABLE `year_levels`
  ADD PRIMARY KEY (`year_level_id`),
  ADD UNIQUE KEY `year_level_name` (`year_level_name`);

--
-- AUTO_INCREMENT for dumped tables
--

--
-- AUTO_INCREMENT for table `books`
--
ALTER TABLE `books`
  MODIFY `book_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=16;

--
-- AUTO_INCREMENT for table `borrow_items`
--
ALTER TABLE `borrow_items`
  MODIFY `borrow_items_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=24;

--
-- AUTO_INCREMENT for table `borrow_transactions`
--
ALTER TABLE `borrow_transactions`
  MODIFY `transaction_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=22;

--
-- AUTO_INCREMENT for table `categories`
--
ALTER TABLE `categories`
  MODIFY `category_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=39;

--
-- AUTO_INCREMENT for table `departments`
--
ALTER TABLE `departments`
  MODIFY `department_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=9;

--
-- AUTO_INCREMENT for table `students`
--
ALTER TABLE `students`
  MODIFY `student_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=16;

--
-- AUTO_INCREMENT for table `users`
--
ALTER TABLE `users`
  MODIFY `user_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=2;

--
-- AUTO_INCREMENT for table `year_levels`
--
ALTER TABLE `year_levels`
  MODIFY `year_level_id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=9;

--
-- Constraints for dumped tables
--

--
-- Constraints for table `books`
--
ALTER TABLE `books`
  ADD CONSTRAINT `fk_book_category` FOREIGN KEY (`category_id`) REFERENCES `categories` (`category_id`);

--
-- Constraints for table `borrow_items`
--
ALTER TABLE `borrow_items`
  ADD CONSTRAINT `fk_item_book` FOREIGN KEY (`book_id`) REFERENCES `books` (`book_id`),
  ADD CONSTRAINT `fk_item_transaction` FOREIGN KEY (`transaction_id`) REFERENCES `borrow_transactions` (`transaction_id`) ON DELETE CASCADE;

--
-- Constraints for table `borrow_transactions`
--
ALTER TABLE `borrow_transactions`
  ADD CONSTRAINT `fk_transaction_student` FOREIGN KEY (`student_id`) REFERENCES `students` (`student_id`),
  ADD CONSTRAINT `fk_transaction_user` FOREIGN KEY (`processed_by`) REFERENCES `users` (`user_id`);

--
-- Constraints for table `students`
--
ALTER TABLE `students`
  ADD CONSTRAINT `fk_student_department` FOREIGN KEY (`department_id`) REFERENCES `departments` (`department_id`),
  ADD CONSTRAINT `fk_student_year_level` FOREIGN KEY (`year_level_id`) REFERENCES `year_levels` (`year_level_id`);
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
