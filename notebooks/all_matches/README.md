# MLS Data Pipeline

This repository contains code for an automated data pipeline that processes Major League Soccer (MLS) match data. The pipeline extracts match information from various sources, transforms it into a structured format, and loads it into a data warehouse using dimensional modeling principles.

The data model includes fact tables for matches and dimension tables for teams, venues, dates, broadcasters, seasons, and competitions. This structure enables efficient querying and analysis of MLS match data across multiple dimensions.


### Fact_Match 

| Column | Data Type | Description |
|--------|-----------|-------------|
| Match_SK | INTEGER (PK) | Surrogate primary key |
| Match_DateTime | TIMESTAMP | Date and time of the match |
| HomeTeamKey | INTEGER | Foreign key to DimTeam |
| AwayTeamKey | INTEGER | Foreign key to DimTeam |
| VenueKey | INTEGER | Foreign key to DimVenue |
| SeasonKey | INTEGER | Foreign key to DimSeason |
| CompetitionKey | INTEGER | Foreign key to DimCompetition |
| BroadcasterKey | INTEGER | Foreign key to DimBroadcaster |
| IsDelayed | BOOLEAN | Whether the match was delayed |
| MatchDay | INTEGER | Matchday number |


<hr>

### DimTeam

```sql
DimTeam (
    TeamKey INT PRIMARY KEY,
    OptaId INT,
    SportecId VARCHAR,
    FullName VARCHAR,
    ShortName VARCHAR,
    Abbreviation VARCHAR,
    BackgroundColor VARCHAR,
    LogoColorUrl VARCHAR
)
```

### DimVenue

```sql
DimVenue (
  VenueKey INTEGER PRIMARY KEY,
  VenueSportecId VARCHAR,
  Name VARCHAR,
  City VARCHAR
)
```

### DimDate

```sql
DimDate (
  DateKey INTEGER PRIMARY KEY, -- YYYYMMDD format
  FullDate DATE,
  Year INTEGER,
  Month INTEGER,
  Day INTEGER,
  Quarter INTEGER,
  Weekday VARCHAR
)
```

### DimBroadcaster

```sql
DimBroadcaster (
  BroadcasterKey INTEGER PRIMARY KEY,
  BroadcasterName VARCHAR,
  BroadcasterType VARCHAR,
  StreamingURL VARCHAR,
  Country VARCHAR
)

```

### DimSeason

```sql
DimSeason (
  SeasonKey INTEGER PRIMARY KEY,
  OptaId INTEGER,
  SeasonSlug VARCHAR,
  Year INTEGER
)
```

### DimCompetition

```sql
DimCompetition (
  CompetitionKey INTEGER PRIMARY KEY,
  OptaId INTEGER,
  Name VARCHAR,
  MatchType VARCHAR,
  Slug VARCHAR
)

```