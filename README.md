# Pràctica 3: Sockets (servidor FTP i clients)

![CFGS DAM](https://img.shields.io/badge/CFGS-Desenvolupament%20d%27Aplicacions%20Multiplataforma%20%28DAM%29-green)
![PSP](https://img.shields.io/badge/assignatura-Programaci%C3%B3%20de%20Serveis%20i%20Processos-teal)

Pràctica 3 de l'assignatura de Programació de Serveis i Processos (PSP) del CFGS de Desenvolupament d'Aplicacions Multiplataforma. Consisteix en un **servidor FTP propi sobre sockets TCP** i dos clients, un per a Linux i un altre per a Windows, escrits en C/C++.

## Components

| Carpeta | Descripció |
|---|---|
| `ClassServer` | Servidor principal orientat a objectes (C++): gestiona diversos clients concurrents amb fils i valida usuaris. |
| `Server` | Servidor FTP en C++ (`servidor_ftp`). |
| `ServidorSimplificat` | Versió mínima del servidor, en C. |
| `ClientLinux` | Client de consola per a Linux. |
| `ClientWin` | Client de consola per a Windows (Winsock). |
| `ftp_root` | Directori arrel que serveix el servidor; els clients no en poden sortir. |
| `bin_linux` | Binaris compilats per a Linux. |

## Protocol

El servidor escolta al port **10235**. Cada petició comença amb una capçalera (`ConnectionHeader`, definida a `ClassServer/Dades.h`) que inclou l'operació, la versió del protocol, les credencials i el camí actual. Les operacions disponibles són:

| Codi | Operació | Descripció |
|---|---|---|
| 1 | `DIR` | Llista el contingut del directori actual. |
| 2 | `CD` | Canvia de directori (sense sortir de `ftp_root`). |
| 3 | `GET` | Descarrega un fitxer. |
| 4 | `RGET` | Descarrega recursivament un directori. |
| 5 | `REGISTRE` | Registra un usuari nou. |
| 99 | `SORTIR` | Tanca la connexió. |

## Compilació i execució

### Linux

```bash
make            # compila servidor i client a bin_linux/
make run_server # en una terminal
make run_client # en una altra
```

Requereix `g++` i suport de `pthread`.

### Windows

Obre `PracticaSockets.slnx` amb Visual Studio i compila els projectes `ClassServer` i `ClientWin`.

## Notes

- La carpeta `readme/` conté documentació de Visual Studio sobre el desenvolupament remot per a Linux, utilitzada per compilar el client Linux des de Windows.
- `imma_make_it_from_zero.txt` conté esbossos de codi (capçaleres) del servidor.
