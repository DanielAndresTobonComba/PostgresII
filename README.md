# PostgresII
~~~sql 
create table pais (
	id serial primary key, 
	nombre varchar(50) unique not null

);

create table departamento (
	id int primary key,
	nombre varchar(50) unique not null,
	idPais int,
	foreign key (idPais) references pais (id)
);

create table municipio (
	id serial  primary key,
	numMunicipio int not null,
	nombre varchar(50) not null,
	idDepartamento int,
	foreign key (idDepartamento) references departamento (id)
	
);

create table localidad (
	idDepartamento int not null ,
	nombreDepartamento varchar (50)not null,
	idMunicipio int not null,
	nombreMunicipio varchar(50) not null
);
~~~


~~~sql
\copy localidad (idDepartamento, nombreDepartamento, idMunicipio, nombreMunicipio )
    from '/home/camper/Escritorio/localidades.csv' WITH DELIMITER ',' CSV HEADER;
    
  
alter table municipio drop constraint nombre;
    
insert into pais (id , nombre ) 
values ( 1 , "Colombia");
    
INSERT INTO departamento (id , nombre , idPais)
SELECT DISTINCT iddepartamento , nombredepartamento  , 1
FROM localidad;


INSERT INTO municipio (numMunicipio , nombre , idDepartamento)
SELECT idMunicipio , nombreMunicipio  , idDepartamento
FROM localidad 
order by idMunicipio;
~~~ 
