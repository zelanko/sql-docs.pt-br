---
title: Atualizado - SQL Server no Linux documentos | Microsoft Docs
description: Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, para o Microsoft SQL Server no Linux.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: linux
ms.date: 04/28/2018
ms.openlocfilehash: adc9b9d4dec86f1b0e8807869aa0f20532837cea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Novos e recentemente atualizado: SQL Server no Linux docs



Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **2018-02-03** &nbsp; - para - &nbsp; **2018-04-28**
- *Área de assunto:* &nbsp; **Microsoft SQL Server no Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Autenticação do Active Directory para o SQL Server no Linux](sql-server-linux-active-directory-auth-overview.md)
2. [Configurar SQL Server sempre no grupo de disponibilidade no Windows e Linux (plataforma cruzada)](sql-server-linux-availability-group-cross-platform.md)
3. [Sempre operam em grupos de disponibilidade no Linux](sql-server-linux-availability-group-operate-ha.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Configure repositórios para instalar e atualizar o SQL Server no Linux](#TitleNum_1)
2. [Configurar o SQL Server no Linux com a ferramenta mssql conf](#TitleNum_2)
3. [Notas de versão do SQL Server 2017 no Linux](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-configure-repositories-for-installing-and-upgrading-sql-server-on-linuxsql-server-linux-change-repomd"></a>1. &nbsp; [Configure repositórios para instalar e atualizar o SQL Server no Linux](sql-server-linux-change-repo.md)

*Atualizado em: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([próxima](#TitleNum_2))

<!-- Source markdown line 72.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5ccaa0fcb8895f25c162e4e0494ad4872773de3 29a959be6ee7d58fe0c53e8f91bdd282fb2e6d29  (PR=5676  ,  Filename=sql-server-linux-change-repo.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- Imprima o conteúdo do arquivo.

```
   sudo cat /etc/yum.repos.d/mssql-server.repo
```

- O **nome** propriedade é o repositório configurado. Você pode identificá-lo com a tabela na seção [repositórios] deste artigo.

**Remover o repositório antigo (RHEL)**

Se necessário, remova o repositório antigo com o comando a seguir.

```
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

Esse comando assume que o arquivo identificado na seção anterior foi denominado **server.repo mssql**.

**Configurar o novo repositório (RHEL)**

Configure o novo repositório a ser usado para atualizações e instalações do SQL Server. Use um dos comandos a seguir para configurar o repositório de sua escolha.

| Repositório | Comando |
|---|---|
| **CU** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

**<a id="sles"></a> Configure os repositórios SLES**

Use as etapas a seguir para configurar os repositórios em SLES.

**Verificar se há repositórios configurados anteriormente (SLES)**

Primeiro, verifique se você já registrou um repositório do SQL Server.

- Use **zypper informações** para obter informações sobre qualquer repositório configurado anteriormente.

```
   sudo zypper info mssql-server
```

- O **repositório** propriedade é o repositório configurado. Você pode identificá-lo com a tabela na seção [repositórios] deste artigo.

**Remover o repositório antigo (SLES)**

Se necessário, remova o repositório antigo. Use um dos comandos a seguir com base no tipo de repositório previamente configurado.

| Repositório | Comando para remover |
|---|---|
| **Visualização** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-sql-server-on-linux-with-the-mssql-conf-toolsql-server-linux-configure-mssql-confmd"></a>2. &nbsp; [Configurar o SQL Server no Linux com a ferramenta mssql conf](sql-server-linux-configure-mssql-conf.md)

*Atualizado em: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [próxima](#TitleNum_3))

<!-- Source markdown line 151.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3664c4d64ea4840dcbc718461ed04403cc486f30 89f708af45ce262057e967e9047f1328e19248ba  (PR=5676  ,  Filename=sql-server-linux-configure-mssql-conf.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->




**<a id="masterdatabasedir"></a> Alterar o local de diretório do arquivo de banco de dados mestre padrão**


O **filelocation.masterdatafile** e **filelocation.masterlogfile** alterações de configuração no local onde o mecanismo do SQL Server procura os arquivos de banco de dados mestre. Por padrão, esse local é /var/opt/mssql/data.

Para alterar essas configurações, use as seguintes etapas:

- Crie o diretório de destino para novos arquivos de log de erro. O exemplo a seguir cria um novo **/tmp/masterdatabasedir** diretório:

```
   sudo mkdir /tmp/masterdatabasedir
```

- Alterar o proprietário e o grupo do diretório para o **mssql** usuário:

```
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
```

- Use mssql conf para alterar o diretório de banco de dados mestre padrão para os arquivos de log e de dados mestre com o **definir** comando:

```
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
```

- Interrompa o serviço do SQL Server:

```
   sudo systemctl stop mssql-server
```

- Mova o master.mdf e masterlog.ldf:

```
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
```

- Inicie o serviço do SQL Server:

```
   sudo systemctl start mssql-server
```

> [!NOTE]
> Se o SQL Server não pode localizar os arquivos do master.mdf e mastlog.ldf no diretório especificado, uma cópia do modelo de bancos de dados do sistema será automaticamente criada no diretório especificado e do SQL Server será inicializada com êxito. No entanto, metadados, como bancos de dados de usuário, os logons de servidor, certificados de servidor, chaves de criptografia, trabalhos do SQL agent ou antiga senha de logon não serão atualizado no novo banco de dados mestre. Você precisará parar o SQL Server e mover seu antigo master.mdf e mastlog.ldf para o novo local especificado e iniciar o SQL Server para continuar usando os metadados existentes.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>3. &nbsp; [Notas de versão do SQL Server 2017 no Linux](sql-server-linux-release-notes.md)

*Atualizado em: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2))

<!-- Source markdown line 64.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 367d112a9427bbdd18e0e52cc82264dd169c91ae 63a67be08fa39ece778cf9ca0b9746dd28694574  (PR=5676  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- [Habilitar o SQL Server Agent]

**<a id="CU6"></a> CU6 (abril de 2018)**


Esta é a versão de atualização cumulativa 6 (CU6) do SQL Server 2017. A versão do mecanismo do SQL Server para esta versão é 14.0.3025.34. Para obter informações sobre as correções e aperfeiçoamentos desta versão, consulte [ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464).

**Detalhes do pacote**


Para instalações de pacote manual ou off-line, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3025.34-3 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[Pacote do SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) |
| Pacote RPM SLES | 14.0.3025.34-3 | [pacote de RPM mecanismo MSSQL server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de alta disponibilidade RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacote de RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) |
| Pacote Debian Ubuntu 16.04 | 14.0.3025.34-3 | [Mecanismo de pacote Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[Pacote Debian do alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[Pacote do SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |







## <a name="similar-articles-about-new-or-updated-articles"></a>Artigos semelhantes sobre artigos novos ou atualizados

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que *têm* artigos novos ou atualizados recentemente

- [Novo + atualizado (11 + 6): &nbsp; &nbsp; **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (18 + 0): &nbsp; &nbsp; **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (218 + 14): **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (14 + 0): &nbsp; &nbsp; **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (3 + 2): &nbsp; &nbsp; **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (3 + 3): &nbsp; &nbsp; **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (7 + 10): &nbsp; &nbsp; **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (0 + 2): &nbsp; &nbsp; **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (1 + 3): &nbsp; &nbsp; **Studio de operações SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + atualizado (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Novo + atualizado (0 + 2): &nbsp; &nbsp; **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Novo + atualizado (1 + 1): &nbsp; &nbsp; **Tools para SQL** documentos](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas de assunto que *não* têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + atualizado (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): **extensões DMX (Data Mining) para o SQL** documentos](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): **MDX (Multidimensional Expressions) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): **ODBC (conectividade aberta de banco de dados) para o SQL** documentos](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): **exemplos para SQL** documentos](../samples/new-updated-samples.md)
- [Novo + atualizado (0 + 0): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 0): **XQuery para o SQL** documentos](../xquery/new-updated-xquery.md)

