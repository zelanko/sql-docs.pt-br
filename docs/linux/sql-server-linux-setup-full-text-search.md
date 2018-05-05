---
title: Instalar a pesquisa de texto completo do SQL Server no Linux | Microsoft Docs
description: Este artigo descreve como instalar a pesquisa de texto completo do SQL Server no Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.openlocfilehash: 7e401f8431ca340d02fd2020431b560dc44c80e1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="install-sql-server-full-text-search-on-linux"></a>Instalar a pesquisa de texto completo do SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

As etapas a seguir instalar [pesquisa de texto completo do SQL Server](https://msdn.microsoft.com/library/ms142571.aspx) (**fts do mssql server**) no Linux. Pesquisa de texto completo permite executar consultas de texto completo em dados baseados em caracteres nas tabelas do SQL Server. Para problemas conhecidos desta versão, consulte o [notas de versão](sql-server-linux-release-notes.md).

> [!NOTE]
> Antes de instalar a pesquisa de texto completo do SQL Server, primeiro [instalar o SQL Server](sql-server-linux-setup.md#platforms). Isso configura as chaves e os repositórios que você usar ao instalar o **fts do mssql server** pacote.

Instale a pesquisa de texto completo do SQL Server para sua plataforma:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">Instalar em RHEL</a>

Use os comandos a seguir para instalar o **fts do mssql server** no Red Hat Enterprise Linux. 

```bash
sudo yum install -y mssql-server-fts
```

Se você já tiver **fts do mssql server** instalado, você pode atualizar a versão mais recente com os seguintes comandos:

```bash
sudo yum check-update
sudo yum update mssql-server-fts
```

Se você precisar de uma instalação offline, localize o download do pacote de pesquisa de texto completo no [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [instalar o SQL Server](sql-server-linux-setup.md#offline).

## <a name="ubuntu">Instalar no Ubuntu</a>

Use os comandos a seguir para instalar o **fts do mssql server** no Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts
```

Se você já tiver **fts do mssql server** instalado, você pode atualizar a versão mais recente com os seguintes comandos:

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts 
```

Se você precisar de uma instalação offline, localize o download do pacote de pesquisa de texto completo no [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [instalar o SQL Server](sql-server-linux-setup.md#offline).

## <a name="SLES">Instalar em SLES</a>

Use os comandos a seguir para instalar o **fts do mssql server** no SUSE Linux Enterprise Server. 

```bash
sudo zypper install mssql-server-fts
```

Se você já tiver **fts do mssql server** instalado, você pode atualizar a versão mais recente com os seguintes comandos:

```bash
sudo zypper refresh
sudo zypper update mssql-server-fts
```

Se você precisar de uma instalação offline, localize o download do pacote de pesquisa de texto completo no [notas de versão](sql-server-linux-release-notes.md). Em seguida, use as mesmas etapas de instalação offline descritas no artigo [instalar o SQL Server](sql-server-linux-setup.md#offline).

## <a name="supported-languages"></a>Idiomas com suporte

Pesquisa de texto completo usa [separadores de palavras](../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) que determinam como identificar palavras individuais com base no idioma. Você pode obter uma lista de separadores de palavras registrados, consultando o **sys. fulltext_languages** exibição do catálogo. Separadores de palavras para os seguintes idiomas são instalados com o SQL Server 2017:

| Idioma | ID de idioma |
|---|---|
| Neutro | 0 |
| Árabe | 1025 |
| Bengali (India) | 1093 |
| Bokmål | 1044 |
| Brasileiro | 1046 |
| British English | 2057 |
| Búlgaro | 1026 |
| Catalão | 1027 |
| Chinês (RAE de Hong Kong, RPC) | 3076 |
| Chinês (RAE de Macau) | 5124 |
| Chinês (Cingapura) | 4100 |
| Croata | 1050 |
| Tcheco | 1029 |
| Danish | 1030 |
| Holandês | 1043 |
| Inglês | 1046 |
| Francês | 1036 |
| Alemão | 1031 |
| Greek | 1032 |
| Guzerati | 1095 |
| Hebraico | 1037 |
| Híndi | 1081 |
| Islandês | 1039 |
| Indonésio | 1057 |
| Italiano | 1040 |
| Japonês | 1041 |
| Kannada | 1099 |
| Coreano | 1042 |
| Letão | 1062 |
| Lituano | 1063 |
| Malay - Malaysia | 1086 |
| Malaiala | 1100 |
| Marati | 1102 |
| Polonês | 1045 |
| Português | 2070 |
| Punjabi | 1094 |
| Romeno | 1048 |
| Russo | 1049 |
| Sérvio (Cirílico) | 3098 |
| Serbian (Latin) | 2074 |
| Chinês simplificado | 2052 |
| Eslovaco | 1051 |
| Esloveno | 1060 |
| Espanhol | 3082 |
| Sueco | 1053 |
| Tâmil | 1097 |
| Télugo | 1098 |
| Tailandês | 1054 |
| Chinês tradicional | 1028 |
| Turco | 1055 |
| Ucraniano | 1058 |
| Urdu | 1056 |
| Vietnamita | 1066 |

## <a id="filters"></a> Filtros

Pesquisa de texto completo também funciona com texto armazenado em arquivos binários. Mas, nesse caso, um filtro instalado é necessária para processar o arquivo. Para obter mais informações sobre filtros, consulte [configurar e gerenciar filtros para pesquisa](../relational-databases/search/configure-and-manage-filters-for-search.md).

Você pode ver uma lista de filtros instalados chamando **sp_help_fulltext_system_components 'filter'**. Para o SQL Server 2017, os filtros a seguir estão instalados:

| Nome do Componente | ID de classe | Versão |
|---|---|---|
|.a | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ANS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.asc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ascx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|. ASM | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|. ASP | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.aspx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|. asx | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.bas | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. bat | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.bcp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. c | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|CLS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cmd | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|. cs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.CSA | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. CSS | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.csv | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dbs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. def | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|. dic | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dos | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. DSP | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|dsw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. ext | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.faq | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.fky | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. h | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.hhc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.hta | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.html | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|htt | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|. htw | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.i | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ibq | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|ICS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. idl | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|IDQ | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. Inc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|. inf | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.ini | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.inl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. inx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.jav | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.java | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. js | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.kci | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.lgN | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.log | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|. lst | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.m3u | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.MAK | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.MK | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.odc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.odh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|odl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgdef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgundef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. pl | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.PRC | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. rc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rc2 | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. rct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. reg | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|. rgs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rtf | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rul | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. s | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.scc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.shtm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.shtml | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|. snippet | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sol | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sor | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.srf | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.stm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|. TAB | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tdl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. TLH | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tli | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.trg | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. txt | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|. udf | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.UDT | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.url | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|. usr | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vbs | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.viw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. VSCT | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsixlangpack | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsixmanifest | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vspscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vssscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wri | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wtx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.xml | 41B9BE05-B3AF-460C-BF0B-2CDD44A093B1 | 12.0.9735.0 |

## <a name="semantic-search"></a>Pesquisa semântica
[A pesquisa semântica](../relational-databases/search/semantic-search-sql-server.md) cria o recurso de pesquisa de texto completo para extrair e índice estatisticamente relevantes *frases-chave*. Isso permite que você consultar o significado dentro de documentos no banco de dados. Ele também ajuda a identificar documentos semelhantes.

Para usar a pesquisa semântica, você deve restaurar primeiro o banco de dados de estatísticas semânticas de idioma para o seu computador.

1. Usar uma ferramenta como [sqlcmd](sql-server-linux-setup-tools.md), para executar o seguinte comando Transact-SQL na instância do SQL Server do Linux. Este comando restaura o banco de dados de estatísticas de idioma.

   ```sql
   RESTORE DATABASE [semanticsdb] FROM
   DISK = N'/opt/mssql/misc/semanticsdb.bak' WITH FILE = 1,
   MOVE N'semanticsdb' TO N'/var/opt/mssql/data/semanticsDB.mdf',
   MOVE N'semanticsdb_log' TO N'/var/opt/mssql/data/semanticsdb_log.ldf', NOUNLOAD, STATS = 5
   GO
   ```

   > [!NOTE]
   > Se necessário, atualize os caminhos no comando de restauração anterior para ajustar sua configuração.

1. Execute o seguinte comando Transact-SQL para registrar o banco de dados de estatísticas semânticas de idioma.

    ```sql
    EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
    GO
    ```

## <a name="next-steps"></a>Próximas etapas

Para obter informações sobre a pesquisa de texto completo, consulte [pesquisa de texto completo do SQL Server](../relational-databases/search/full-text-search.md). 
