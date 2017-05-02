-- Table structure for course
CREATE TABLE `mytest0721`.`course` (
  `cno` VARCHAR(10) NOT NULL,
  `cname` VARCHAR(25) NOT NULL,
  `tno` VARCHAR(20) NULL DEFAULT NULL,
  PRIMARY KEY (`cno`, `cname`));

-- Records of course
INSERT INTO `course` VALUES ('c001', 'J2SE', 't002');
INSERT INTO `course` VALUES ('c002', 'Java Web', 't002');
INSERT INTO `course` VALUES ('c003', 'SSH', 't001');
INSERT INTO `course` VALUES ('c004', 'Oracle', 't001');
INSERT INTO `course` VALUES ('c005', 'SQL SERVER 2005', 't003');
INSERT INTO `course` VALUES ('c006', 'C#', 't003');
INSERT INTO `course` VALUES ('c007', 'javascript', 't002');
INSERT INTO `course` VALUES ('c008', 'DIV+CSS', 't001');
INSERT INTO `course` VALUES ('c009', 'PHP', 't003');
INSERT INTO `course` VALUES ('c010', 'EJB3.0', 't002');

-- Table structure for sc

CREATE TABLE `sc` (
  `sno` varchar(10) NOT NULL,
  `cno` varchar(10) NOT NULL,
  `score` float(4,2) DEFAULT NULL,
  PRIMARY KEY (`sno`,`cno`));

-- Records of sc
INSERT INTO `sc` VALUES ('s001', 'c001', '78.90');
INSERT INTO `sc` VALUES ('s002', 'c001', '80.90');
INSERT INTO `sc` VALUES ('s003', 'c001', '81.90');
INSERT INTO `sc` VALUES ('s004', 'c001', '60.90');
INSERT INTO `sc` VALUES ('s001', 'c002', '82.90');
INSERT INTO `sc` VALUES ('s002', 'c002', '72.90');
INSERT INTO `sc` VALUES ('s003', 'c002', '81.90');
INSERT INTO `sc` VALUES ('s001', 'c003', '59.00');

-- Table structure for student
CREATE TABLE `mytest0721`.`student` (
  `sno` VARCHAR(10) NOT NULL,
  `sname` VARCHAR(20) NULL DEFAULT NULL,
  `sage` int(2) NULL DEFAULT NULL,
  `ssex` VARCHAR(5) NULL DEFAULT NULL,
  PRIMARY KEY (`sno`));


-- Records of student
INSERT INTO `student` VALUES ('s001', '張三', '23', '男');
INSERT INTO `student` VALUES ('s002', '李四', '23', '男');
INSERT INTO `student` VALUES ('s003', '吳鵬', '25', '男');
INSERT INTO `student` VALUES ('s004', '琴沁', '20', '女');
INSERT INTO `student` VALUES ('s005', '王麗', '20', '女');
INSERT INTO `student` VALUES ('s006', '李波', '21', '男');
INSERT INTO `student` VALUES ('s007', '劉玉', '21', '男');
INSERT INTO `student` VALUES ('s008', '蕭蓉', '21', '女');
INSERT INTO `student` VALUES ('s009', '陳蕭曉', '23', '女');
INSERT INTO `student` VALUES ('s010', '陳美', '22', '女');

-- Table structure for teacher
CREATE TABLE `mytest0721`.`teacher` (
    `tno` VARCHAR(10) NOT NULL,
    `tname` VARCHAR(20) NULL DEFAULT NULL,
    PRIMARY KEY (`tno`)
);

-- Records of teacher
INSERT INTO `teacher` VALUES ('t001', '劉陽');
INSERT INTO `teacher` VALUES ('t002', '諶燕');
INSERT INTO `teacher` VALUES ('t003', '胡明星');
