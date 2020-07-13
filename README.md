# Kesepakatan Standar Pedoman Umum Pengembangan Aplikasi
[Refer to ISO/IEC_9126](https://en.wikipedia.org/wiki/ISO/IEC_9126)


Revision History

| Tanggal      | Versi 	| Deskripsi  					|
| ------------ |--------| ------------------------------|
| 07 Juli 2020 | 0.1 	| Pembuatan awal dokumentasi	|

Daftar Isi :

 1. [Repository Convention (Kesepakatan Repository)](#1-repository-convention)
 2. [Database Convention (Kesepakatan Database)](#2-database-convention)
 3. [Programming Convention (Kesepakatan Pemrograman)](#3-programming-convention)
 4. [Documentation Convention (Kesepakatan Dokumentasi)](#4-documentation-convention)

# 1. Repository-Convention #
 1. Repository setiap project internal ATT Group diharuskan menggunakan server gitlab internal yaitu : gitlab.att-group.co.id
 2. Penulisan group, sub group dan project disarankan menggunakan huruf kecil tanpa spasi agar memudahkan penanganan jika dipergunakan di sistem operasi lama (legacy system).
 3. Untuk setiap project disarankan menggunakan group dan atau sub group dimana repository dimaksud ada didalam group dan atau sub group, hal ini agar memudahkan administrasi hak akses dan dokumentasi. Contoh :
https://gitlab.att-group.co.id/group-frontend/reactjs/template/metronic7.git
 4. Struktur git repo
    - group-frontend (group)
	    - reactjs (sub group)
		    - template (sub group)	
			    - metronic7 (project repo)
			    - adminlte (project repo)
		- transys (sub group)	
		    - transys1 (project repo)
			- transys2 (project repo)
		 - vuejs (sub group)
			 - template (sub group)	
				 - metronic7 (project repo)
				 - adminlte (project repo)
 5. Setiap Project sangat disarankan menggunakan metode feature dan merging ke developement  dan production untuk branch nya, hal ini agar ci/cd dapat berjalan dengan baik, contoh:
    - **Project A**
        - **production** branch
        - **development** branch ↑ merge request to production
        - feature-a branch ↑ merge request to development
        - feature-b branch ↑ merge request to development

 6. Sangat disarankan untuk praktek automatic ci/cd dijalankan agar deployment ke server baik itu development dan production tidak menggunakan ftp/sftp atau akses langsung developer ke server.

# 2. Database-Convention #

**MySQL/MariaDB**
> User
> Databases
>> Table/object2 database

**PostgreSQL**
> User
> Databases
>> Schema
>>> Table/object2 database

**Oracle**
> Database Instance
>> User/Schema
>>> Table/object2 database

**Structured Database (MySQL, MariaDB & PostgreSQL)**
1. Hak Akses Databases
	1. Databases
		1. MySQL, MariaDB
			1. Production, untuk penamaan misal finance
			2. Development, untuk penamaan ditambahkan dev pada akhir nama database misal financedev
		2. PostgreSQL
			1. Production, untuk schema penampung object2 production
			2. Development, untuk schema penampung object2 development
	2. User (MySQL, MariaDB & PostgreSQL)
		1. Development, hak akses untuk object2 development 
		2. Production, hak akses untuk object2 production 
	3.  Schema (PostgreSQL & Oracle)
		1. Akses ke schema diberikan sesuai dengan kebutuhan project dan lingkungannya (production atau development)
		2. Object yang specific project harus dibuat dalam schema yang dimaksud
2. Penamaan Object
	1. Table, Nama table sebaiknya merujuk pada ketentuan bersama untuk project dimaksud, contoh :
			1. master data (3 karakter di depan mda) -> tb_mda_namatable
			2. child / detail / turunan , bisa merujuk pada penomoran -> tb_mda_namatable_dtl01, tb_mda_namatable_dtl02 dst.
	2. View, Nama view sebaiknya merujuk pada ketentuan bersama untuk project dimaksud ditambahkan 2 karakter di depan sebagai penanda object view -> vw_namaview
	3. Materialized View (PostgreSQL & Oracle), Nama materialized view sebaiknya merujuk pada ketentuan bersama untuk project dimaksud ditambahkan 2 karakter di depan sebagai penanda object materialized view -> mv_namamaterializedview
	4. Type (PostgreSQL & Oracle), Nama Type sebaiknya merujuk pada ketentuan bersama untuk project dimaksud ditambahkan 2 karakter di depan sebagai penanda object type -> ty_namatype
	5. Triggers, Nama Triggers sebaiknya merujuk pada ketentuan bersama untuk project dimaksud ditambahkan 2 karakter di depan sebagai penanda object Triggers -> tg_namatriggers
	6. Function, Nama Function sebaiknya merujuk pada ketentuan bersama untuk project dimaksud ditambahkan 2 karakter di depan sebagai penanda object Function -> fn_namafunction
	7.  Procedure (PostgreSQL & Oracle), Nama Procedure sebaiknya merujuk pada ketentuan bersama untuk project dimaksud ditambahkan 2 karakter di depan sebagai penanda object Procedure -> pr_namaprocedure
	8. Sequence (PostgreSQL & Oracle), Nama Sequence sebaiknya merujuk pada ketentuan bersama untuk project dimaksud ditambahkan 2 karakter di depan sebagai penanda object Sequence -> sq_namasequence
	9. Index, Nama Index sebaiknya merujuk pada ketentuan bersama untuk project dimaksud ditambahkan 2 karakter di depan sebagai penanda object Index -> ix_namaindex
	10. Partitions (PostgreSQL & Oracle), Nama Partitions sebaiknya merujuk pada ketentuan bersama untuk project dimaksud ditambahkan 2 karakter di depan sebagai penanda object Partitions -> pt_namapartitions
	11. Constraints
		1. Primary Key (pk_namatablenamaprimarykey)
		2. Unique Key (uk_namatablenamauniquekey)
		3. Foreign Key (fk_namatablenamaforeignkey)
		4. Check/Validation (ck_namatablenamacheckvalidation)
	12. Scheduler (PostgreSQL & Oracle) (sj_namaschedulerjob)
3. Penamaan Kolom, Nama kolom sebaiknya merujuk pada ketentuan bersama untuk project dimaksud ditambahkan dengan mempertimbangkan kemudahan baca (readability), tidak perlu dipersingkat nama kolom jika memungkinkan, contoh : 
> tb_mdm_trxcashjournal (nama tabel)
> > trxcashjournal_code varchar(60), 
> > trxcashjournal_branchcode varchar(60),
> > trxcashjournal_totalamount integer
4. Tipe Data
	1. Karakter
		1. varchar (MySQL & PostgreSQL) minimal 30 maksimum 4,000 
		2. varchar2 (Oracle) minimal 30 maksimum 4,000
		3. text (MySQL & PostgreSQL) minimal 4001 maksimum 65,000
		4. text (Oracle) minimal 4001 maksimum 65,000
	2. Angka
		1. integer (MySQL & Oracle)
		2. int4 (PostgreSQL)
		3. numeric (MySQL & PostgreSQL)
		4. number (Oracle) 
	3. Tanggal
		1. date
	4. Tanggal dan Waktu
		1. timestamp (PostgreSQL & Oracle)
		2. datetime (MySQL)
	5. Boolean (MySQL & PostgreSQL)
5. Audit DDL
6. Audit DML

**UnStructured Database (MongoDB/NoSQL)**
1. to be discussed
2. to be discussed

# 3. Programming-Convention #
[Refer to Coding conventions](https://en.wikipedia.org/wiki/Coding_conventions)
1. [Refer to PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md)
2. [Refer to PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md)
3. [Refer to PSR-12](https://www.php-fig.org/psr/psr-12/)
4. [PHPDoc](https://github.com/php-fig/fig-standards/blob/master/proposed/phpdoc.md)

# 4. Documentation-Convention #
1. Project task manage on [Trello](trello.com)
2. Issue manage on [gitlab](git.ack.id)
3. Minute Of Meeting (please do write this and attached to the proper project)
	- [Minute Of Meeting](https://en.wikipedia.org/wiki/Minutes)
	- [Sample maybe?](https://templates.office.com/en-us/meeting-minutes-simple-tm00002017)
4. Business Flow Process
    - [Business Process Mapping](https://en.wikipedia.org/wiki/Business_process_mapping) 
    - [Business Flow Process](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/business-process-flows-overview#:~:text=With%20business%20process%20flows%2C%20you,using%20the%20Next%20Stage%20button.)
5. Business Requirement Document (BRD)
	- [Business Requirement](https://en.wikipedia.org/wiki/Business_requirements)
	- [Sample maybe ?](https://its.sfsu.edu/sites/default/files/SFSU%20Business%20Requirements%20Template%20v1.7.docx)
6. System Flow Process / Process Flow Diagram
	- [Process Flow Diagram](https://en.wikipedia.org/wiki/Process_flow_diagram)
	- [Sample Maybe?](https://seilevel.com/business-analyst-resources/business-requirements-models-templates/system-flow/#:~:text=System%20Flows%20are%20systems%20models,and%20decisions%20that%20systems%20execute.&text=They%20are%20very%20similar%20to,to%20document%20a%20system's%20actions.)
7. [Functional Specification](https://en.wikipedia.org/wiki/Functional_specification) Document (FSD)
	- [Sample Maybe?](https://kisd.de/~tom/ia/downloads/andere_func_spec_tutorial.pdf)
8. Data Flow Process / [Data Flow Diagram](https://www.cs.uct.ac.za/mit_notes/software/pdfs/Chp06.pdf)
	- [Data Flow Diagram](https://en.wikipedia.org/wiki/Data-flow_diagram)
	- [Data Flow Diagram](https://www.visual-paradigm.com/guide/data-flow-diagram/what-is-data-flow-diagram/#:~:text=Also%20known%20as%20DFD%2C%20Data,divided%20into%20logical%20and%20physical.)
9. Deployment Flow Process
	- [Release And Deployment Management](https://wiki.en.it-processmaps.com/index.php/Release_and_Deployment_Management)
	- [Release Management Process Flow](https://www.itil-docs.com/release-management-process-flow/)
10. User Acceptance Test (UAT)
	- [Acceptance Testing](https://en.wikipedia.org/wiki/Acceptance_testing)
	- [Sample Maybe?](https://www.vic.gov.au/sites/default/files/2018-09/UAT%20Template.xlsx)
	- [Sample Maybe?](https://tech.sfsu.edu/sites/default/files/SFSU%20User%20Acceptance%20Test%20Plan%20Template%20v1.5.pdf)


