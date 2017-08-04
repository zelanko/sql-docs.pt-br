---
title: Atualizado - SQL Server no Linux documentos | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado para alterados recentemente na documentação, para o Microsoft SQL Server no Linux."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: rothja
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: linux-sql
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/17/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 13c237af359c543f6a99a0fce101af81b5eb2bcf
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Novos e recentemente atualizado: SQL Server no Linux docs



Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **2017-05-23** &nbsp; - para - &nbsp; **2017-07-17**
- *Área de assunto:* &nbsp; **Microsoft SQL Server no Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Executar a imagem de contêiner de 2017 do SQL Server com o Docker](quickstart-install-connect-docker.md)
2. [Instalar o SQL Server e criar um banco de dados no Red Hat](quickstart-install-connect-red-hat.md)
3. [Instalar o SQL Server e criar um banco de dados no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
4. [Instalar o SQL Server e criar um banco de dados no Ubuntu](quickstart-install-connect-ubuntu.md)
5. [Exemplo: De script de instalação autônoma do SQL Server para Red Hat Enterprise Linux](sample-unattended-install-redhat.md)
6. [Exemplo: De script de instalação autônoma do SQL Server para SUSE Linux Enterprise Server](sample-unattended-install-suse.md)
7. [Exemplo: De script de instalação autônoma do SQL Server para Ubuntu](sample-unattended-install-ubuntu.md)
8. [Autenticação do Active Directory com o SQL Server no Linux](sql-server-linux-active-directory-authentication.md)
9. [Alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md)
10. [Configurar imagens de contêiner de 2017 do SQL Server no Docker](sql-server-linux-configure-docker.md)
11. [Comentários do cliente para o SQL Server no Linux](sql-server-linux-customer-feedback.md)
12. [Criptografar conexões ao SQL Server no Linux](sql-server-linux-encrypted-connections.md)
13. [Instalar o SQL Server Integration Services (SSIS) no Linux](sql-server-linux-setup-ssis.md)




&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compact fornece links para todos os artigos atualizados que estão listados na seção foram extraídas.



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados a partir de artigos que encontraram recentemente uma atualização grande.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-configure-sles-cluster-for-sql-server-availability-groupsql-server-linux-availability-group-cluster-slesmd"></a>1. &nbsp;[Configurar SLES Cluster para o grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-sles.md)

*Updated: 2017-06-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 189.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f8d28af253be1dc67615f1ea04135b2f6dff3b71 8be07deddcf0c348d75bf5b4f44615c2383e0722  (PR=2150  ,  Filename=sql-server-linux-availability-group-cluster-sles.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=6dccaff93a6c8b2374a1fad069b2f597898802fc) -->



**Defina a propriedade cluster Iniciar falha-for-fatal como false**


`Start-failure-is-fatal`Indica se uma falha ao iniciar um recurso em um nó adicional impede as tentativas de iniciar nesse nó. Quando definido como `false`, o cluster decidirá se deseja tentar iniciar no mesmo nó novamente com base no limite do recurso atual falha contagem e a migração. Portanto, após o failover, Pacemaker tentará iniciar o recurso de grupo de disponibilidade no primeiro primário depois que a instância do SQL está disponível. Pacemaker cuidará de rebaixamento a réplica secundária e ele será automaticamente reingressar no grupo de disponibilidade. Além disso, se `start-failure-is-fatal` é definido como `false`, o cluster voltará para os limites de failcount configurado configurados com o limite de migração, você precisa fazer se padrão para o limite de migração é atualizado adequadamente.

Para atualizar o valor da propriedade para executar false:
```
sudo crm configure property start-failure-is-fatal=false
sudo crm configure rsc_defaults migration-threshold=5000
```
Se a propriedade tem o valor padrão de `true`, se a primeira tentativa de iniciar o recurso falhar, a intervenção do usuário é necessária após um failover automático para a contagem de falhas do recurso de limpeza e redefinir a configuração usando: `sudo crm resource cleanup <resourceName>` comando.

Para obter mais detalhes sobre propriedades do cluster Pacemaker consulte [configurar recursos de Cluster](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html).

**Configurar isolamento (STONITH)**

Fornecedores de cluster pacemaker exigem STONITH esteja habilitado e um dispositivo de isolamento configurado para uma configuração de cluster com suporte. Quando o Gerenciador de recursos de cluster não é possível determinar o estado de um nó ou de um recurso em um nó, o isolamento é usado para colocar o cluster para um estado conhecido novamente.
Isolamento de nível de recurso principalmente garante que não há nenhuma corrupção de dados em caso de uma interrupção ao configurar um recurso. Você pode usar o isolamento de nível de recurso, por exemplo, o link de comunicação com DRBD (Distributed replicados o dispositivo de bloco) para marcar o disco em um nó como desatualizado quando fica inoperante.




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>2. &nbsp;[Notas de versão do SQL Server 2017 no Linux](sql-server-linux-release-notes.md)

*Updated: 2017-06-20* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1))

<!-- Source markdown line 156.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 684da20f7834000886d7a93f83563c55dc3cf9a6 8597bcde7e5754bb7f38de1ec980027245dac6e5  (PR=2115  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=424a23fd98876db808b91f017e7acbcb5b4daa45) -->



**SQL Server Integration Services (SSIS)**

Você pode executar pacotes SSIS no Linux. Para obter mais informações, consulte o [anúncio de postagem de blog SSIS oferecem suporte para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/). Observe os seguintes problemas conhecidos com esta versão.

- O **mssql servidor é** pacote só tem suporte no Ubuntu neste momento.

- Não há suporte para os seguintes recursos durante a execução de pacotes do SSIS no Linux:
  - Banco de dados de catálogo do SSIS
  - Agendar a execução de pacotes pelo SQL Agent
  - Autenticação do Windows
  - Componentes de terceiros
  - Drivers ODBC de terceiros
  - O Gerenciador de Conexão do ODBC, origem e destino (compatível com o SSIS na atualização do Linux CTP 2.1)
  - Change Data Capture (CDC)
  - Escalar horizontalmente
  - Feature Pack do Azure
  - Hadoop e HDFS suporte
  - Microsoft Connector for SAP BW

Com o SSIS na atualização do Linux CTP 2.1, seus pacotes SSIS podem usar conexões ODBC no Linux. Para obter mais informações, consulte o [postagem do blog anunciar suporte a ODBC no Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).





<a name="similars2"/>

&nbsp;

## <a name="similar-articles"></a>Artigos semelhantes

Esta seção lista os artigos muito semelhantes para artigos atualizados recentemente em outras áreas de assunto, dentro do mesmo repositório GitHub.com: [MicrosoftDocs /**sql de documentos de pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170717-1101  -->

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + atualizados (4 + 4): **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (2 + 0): **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (1 + 2): **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (6 + 0): **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (13 + 2): **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (1 + 0): **Master Data Services (MDS) para SQL** documentos](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (1 + 0): **ODBC (conectividade aberta de banco de dados) para o SQL** documentos](../odbc/new-updated-odbc.md)
- [Novo + atualizado (8 + 4): **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (2 + 2): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (0 + 1): **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Novo + atualizado (1 + 0): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Novo + atualizado (1 + 0): **Tools para SQL** documentos](../tools/new-updated-tools.md)


#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhuma artigos novos ou atualizados recentemente

- [Novo + atualizado (0 + 0): **ActiveX Data Objects (ADO) para o SQL** documentos](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): **extensões DMX (Data Mining) para o SQL** documentos](../dmx/new-updated-dmx.md)
- [Novo + atualizado (0 + 0): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (0 + 0): **MDX (Multidimensional Expressions) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (0 + 0): **exemplos para SQL** documentos](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (0 + 0): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 0): **XQuery para o SQL** documentos](../xquery/new-updated-xquery.md)


&nbsp;


