#### Домашнее задание по теме «Проектирование БД. Связи. 3НФ»
студент: Сергей Романов

группа: SQLPY-1

Проект БД:

![Проект БД](https://github.com/romauov/SQLPY-1--DB-design-and-queries/blob/master/DB%20design.jpg)

SQL запросы:
```
create table if not exists Genre (
	GenreID integer unique,
	GenreName varchar(20) unique
);

create table if not exists Artist (
	ArtistID serial primary key,
	Name varchar(20) unique
);

create table if not exists Album (
	AlbumID integer unique,
	AlbumName varchar(40) not null,
	Year integer check(Year > 1887),
	GenreID integer references Genre(GenreID)
);

create table if not exists Track (
	TrackID integer unique,
	TrackName varchar(30) not null,
	TrackLength integer not null,
	AlbumID integer references Album(AlbumID)	
);

create table if not exists Collection (
	CollectionID integer unique,
	Name varchar(80) not null,
	Year integer check(Year > 1887)
);

create table if not exists GenreArtist (
	GenreID integer references Genre(GenreID),
	ArtistID integer references Artist(ArtistID),
	constraint GA primary key (GenreID, ArtistID)
);

create table if not exists ArtistAlbum (
	AlbumID integer references Album(AlbumID),
	ArtistID integer references Artist(ArtistID),
	constraint AA primary key (AlbumID, ArtistID)
);

create table if not exists CollectionTracks (
	CollectionID integer references Collection(CollectionID),
	TrackID integer references Track(TrackID),
	constraint CT primary key (CollectionID, TrackID)
);
```