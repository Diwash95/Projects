# Projects
CREATE TABLE `appointment` (
  `Appointment_id` int NOT NULL,
  `Date` date DEFAULT NULL,
  `Appointment_Reason` varchar(45) DEFAULT NULL,
  `Appointment_Time` varchar(45) DEFAULT NULL,
  `Reception_number` int NOT NULL,
  PRIMARY KEY (`Appointment_id`),
  KEY `Reception_number` (`Reception_number`),
  CONSTRAINT `appointment_ibfk_1` FOREIGN KEY (`Reception_number`) REFERENCES `reception` (`Reception_number`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
CREATE TABLE `bill` (
  `Bill_number` int NOT NULL,
  `Bill_payment` double DEFAULT NULL,
  `Bill_Balance` double NOT NULL,
  `Bill_status` varchar(45) NOT NULL,
  `Bill_date` date NOT NULL,
  `Room_number` int NOT NULL,
  PRIMARY KEY (`Bill_number`),
  KEY `Room_number` (`Room_number`),
  CONSTRAINT `bill_ibfk_1` FOREIGN KEY (`Room_number`) REFERENCES `room` (`Room_number`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
CREATE TABLE `department` (
  `Department_id` int NOT NULL,
  `Department_name` varchar(45) NOT NULL,
  `Department_head` varchar(45) NOT NULL,
  `Lab_number` int NOT NULL,
  PRIMARY KEY (`Department_id`),
  KEY `Lab_number` (`Lab_number`),
  CONSTRAINT `department_ibfk_1` FOREIGN KEY (`Lab_number`) REFERENCES `laboratory` (`Lab_number`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
CREATE TABLE `doctor` (
  `Doctor_id` int NOT NULL,
  `First_name` varchar(45) NOT NULL,
  `Last_name` varchar(45) DEFAULT NULL,
  `Age` int DEFAULT NULL,
  `Gender` varchar(45) DEFAULT NULL,
  `Contact` varchar(45) DEFAULT NULL,
  `Address` varchar(45) DEFAULT NULL,
  `Doctor_charge` double DEFAULT NULL,
  `Department_id` int NOT NULL,
  PRIMARY KEY (`Doctor_id`),
  KEY `Department_id` (`Department_id`),
  CONSTRAINT `doctor_ibfk_1` FOREIGN KEY (`Department_id`) REFERENCES `department` (`Department_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
CREATE TABLE `laboratory` (
  `Lab_number` int NOT NULL,
  `Lab_date` date DEFAULT NULL,
  `Lab_charge` double NOT NULL,
  `Lab_head` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`Lab_number`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
CREATE TABLE `patient` (
  `Patient_id` int NOT NULL,
  `First_name` varchar(45) NOT NULL,
  `Last_name` varchar(45) DEFAULT NULL,
  `Age` int DEFAULT NULL,
  `Gender` varchar(45) DEFAULT NULL,
  `Contact` int DEFAULT NULL,
  `Address` varchar(45) DEFAULT NULL,
  `Doctor_id` int NOT NULL,
  `Disease` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`Patient_id`),
  KEY `Doctor_id` (`Doctor_id`),
  CONSTRAINT `patient_ibfk_1` FOREIGN KEY (`Doctor_id`) REFERENCES `doctor` (`Doctor_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
CREATE TABLE `reception` (
  `Reception_number` int NOT NULL,
  `Visitor_name` varchar(45) NOT NULL,
  `Contact` varchar(45) DEFAULT NULL,
  `Visit_date` date NOT NULL,
  `Visit_time` varchar(45) NOT NULL,
  `Visit_Reason` varchar(45) NOT NULL,
  PRIMARY KEY (`Reception_number`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
CREATE TABLE `record` (
  `Record_number` int NOT NULL,
  `Patient_id` int NOT NULL,
  `Bill_number` int NOT NULL,
  `Record_date` date NOT NULL,
  `Medical_note` varchar(45) DEFAULT NULL,
  `Emergency_contact` varchar(45) NOT NULL,
  PRIMARY KEY (`Record_number`,`Patient_id`),
  KEY `Patient_id` (`Patient_id`),
  KEY `Bill_number` (`Bill_number`),
  CONSTRAINT `record_ibfk_1` FOREIGN KEY (`Patient_id`) REFERENCES `patient` (`Patient_id`),
  CONSTRAINT `record_ibfk_2` FOREIGN KEY (`Bill_number`) REFERENCES `bill` (`Bill_number`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
CREATE TABLE `room` (
  `Room_number` int NOT NULL,
  `Room_type` varchar(45) NOT NULL,
  `Room_status` varchar(45) NOT NULL,
  `Room_charge` double NOT NULL,
  PRIMARY KEY (`Room_number`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
