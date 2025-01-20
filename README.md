# docker-cheat-sheet

Eine Liste der wichtigsten Dockerfile-Keywords zusammen mit einer kurzen Beschreibung:

## FROM
Definiert das Basis-Image, auf dem alle weiteren Befehle aufbauen.
```dockerfile
FROM <image>[:<tag>]
```

## RUN
Führt einen Befehl aus und erstellt eine neue Schicht im Image.
```dockerfile
RUN <command>
```

## CMD
Gibt den Standardbefehl an, der beim Starten eines Containers ausgeführt wird.
```dockerfile
CMD ["executable", "param1", "param2"]
```

## ENTRYPOINT
Legt den Einstiegspunkt für den Container fest. Ähnlich wie CMD, aber schwerer zu überschreiben.
```dockerfile
ENTRYPOINT ["executable", "param1"]
```

## WORKDIR
Setzt das Arbeitsverzeichnis für nachfolgende Befehle wie RUN, CMD, ENTRYPOINT.
```dockerfile
WORKDIR /path/to/directory
```

## COPY
Kopiert Dateien oder Verzeichnisse vom Build-Kontext ins Image.
```dockerfile
COPY <src> <dest>
```

## ADD
Ähnlich wie COPY, unterstützt jedoch zusätzlich das Entpacken von Archiven und das Herunterladen von URLs.
```dockerfile
ADD <src> <dest>
```

## ENV
Setzt Umgebungsvariablen, die zur Laufzeit des Containers verfügbar sind.
```dockerfile
ENV <key>=<value>
```

## EXPOSE
Deklariert die Ports, die der Container zur Verfügung stellt (informativ).
```dockerfile
EXPOSE <port> [<port>...]
```

## VOLUME
Definiert ein Verzeichnis als Volume, das von außen gemountet werden kann.
```dockerfile
VOLUME ["/path/to/volume"]
```

## ARG
Definiert Build-Argumente, die zur Build-Zeit übergeben werden können.
```dockerfile
ARG <name>[=<default_value>]
```

## LABEL
Fügt Metadaten zum Image hinzu, z. B. Autor oder Version.
```dockerfile
LABEL <key>=<value>
```

## USER
Legt den Benutzer fest, unter dem nachfolgende Befehle ausgeführt werden.
```dockerfile
USER <username>[:<group>]
```

## ONBUILD
Definiert Trigger, die ausgeführt werden, wenn ein abgeleitetes Image erstellt wird.
```dockerfile
ONBUILD <instruction>
```

## HEALTHCHECK
Definiert eine Prüfung, um den Gesundheitszustand des Containers zu überwachen.
```dockerfile
HEALTHCHECK [OPTIONS] CMD <command>
```

## SHELL
Legt die Shell fest, die für Befehle wie RUN verwendet wird.
```dockerfile
SHELL ["executable", "parameters"]
```

## STOP SIGNAL
Gibt das Signal an, das Docker verwendet, um den Container zu stoppen.
```dockerfile
STOPSIGNAL <signal>
```

## MAINTAINER (veraltet)
Gibt den Ersteller des Dockerfiles an. Sollte durch LABEL ersetzt werden.
```dockerfile
MAINTAINER <name>
```

## COPY --chown
Kopiert Dateien oder Verzeichnisse und setzt gleichzeitig den Besitzer und die Gruppe.
```dockerfile
COPY --chown=<user>:<group> <src> <dest>
```

## ADD --chown
Ähnlich wie COPY --chown, unterstützt jedoch zusätzlich das Entpacken von Archiven und das Herunterladen von URLs.
```dockerfile
ADD --chown=<user>:<group> <src> <dest>
```

## CACHEBUST
Eine Technik, um den Build-Cache für bestimmte Befehle zu invalidieren, oft durch Hinzufügen einer Argument-Variable.
```dockerfile
ARG CACHEBUST=1
RUN curl -o /file https://example.com/resource?cachebust=$CACHEBUST
```

## CROSS-STAGE BUILDS
Ermöglicht das Übergeben von Artefakten zwischen verschiedenen Build-Stages.
```dockerfile
COPY --from=<stage> <src> <dest>
```

## MULTI-STAGE BUILDS
Reduziert die Größe des finalen Images durch die Nutzung mehrerer Build-Stages.
```dockerfile
FROM <image> as builder
RUN make /app

FROM <image>
COPY --from=builder /app /app
```

## COMMENT
Kommentare werden in Dockerfiles mit `#` definiert und haben keine Auswirkung auf den Build-Prozess.
```dockerfile
# Das ist ein Kommentar
```
