---
title: "Atualizado – Documentos do Integration Services para SQL Server | Microsoft Docs"
description: "Exiba trechos do conteúdo atualizado com alterações recentes na documentação do Integration Services para Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.workload: integration-services
ms.openlocfilehash: 9660fa7239c14c3adc963cc75ceb98de8316734c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-integration-services-for-sql-server"></a>Novo e atualizado recentemente: Integration Services para SQL Server



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **28-09-2017** &nbsp; a &nbsp; **02-12-2017**
- *Área de assunto:* &nbsp; **Integration Services para SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Armazene e recupere arquivos em compartilhamentos de arquivos local e no Azure com o SSIS](lift-shift/ssis-azure-files-file-shares.md)
2. [Valide pacotes do SSIS implantados no Azure](lift-shift/ssis-azure-validate-packages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Gerenciador de Conexões do Hadoop](#TitleNum_1)
2. [Conecte-se às fontes de dados e aos compartilhamentos de arquivo do Azure locais com a Autenticação do Windows](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-hadoop-connection-managerconnection-managerhadoop-connection-managermd"></a>1. &nbsp; [Gerenciador de Conexões do Hadoop](connection-manager/hadoop-connection-manager.md)

*Atualizado: 28-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Próximo](#TitleNum_2))

<!-- Source markdown line 65.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2d68f4e884304f1a28045b42b680c15cc6a41ec5 fb2429466ea4d545682975d8dbea47451ce98ec7  (PR=4113  ,  Filename=hadoop-connection-manager.md  ,  Dirpath=docs\integration-services\connection-manager\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



**Conecte-se com a autenticação Kerberos**

Há duas opções para configurar o ambiente local. Assim, você pode usar a Autenticação Kerberos com o Gerenciador de Conexões do Hadoop. Você pode escolher a opção que melhor se ajusta às suas circunstâncias.
-   Opção 1: [ingressar o computador do SSIS ao realm do Kerberos–#kerberos-adicionar-realm)
-   Opção 2: [habilitar a confiança mútua entre o domínio do Windows e o realm do Kerberos–#kerberos confiança-mútua)

**<a name="kerberos-join-realm"></a>Opção 1: ingressar o computador do SSIS ao realm do Kerberos**


**Requisitos:**


-   O computador do gateway precisa ingressar o realm do Kerberos e não pode ingressar em nenhum domínio do Windows.

**Como configurar:**


**No computador do SSIS:**

1.  Execute o utilitário **Ksetup** para configurar o realm e servidor KDC do Kerberos.

    O computador deve estar configurado como um membro de um grupo de trabalho, já que o realm do Kerberos é diferente de um domínio do Windows. Defina o realm do Kerberos e adicione um servidor KDC, conforme mostrado no exemplo a seguir. Substitua o *REALM.COM* com seu respectivo realm, conforme necessário.

```
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
```

    Restart the computer after executing these two commands.

2.  Verifique a configuração com o comando **Ksetup**. A saída deverá ser semelhante a esta amostra:

```
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
```

**<a name="kerberos-mutual-trust"></a>Opção 2: habilitar a confiança mútua entre o domínio do Windows e o realm do Kerberos**


**Requisitos:**

-   O computador do gateway deve ingressar em um domínio do Windows.
-   Você precisa de permissão para atualizar as configurações do controlador de domínio.

**Como configurar:**


> [!NOTE]
> Substitua o REALM.COM e o AD.COM no tutorial a seguir com seus respectivos realm e controlador de domínio, conforme necessário.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authenticationlift-shiftssis-azure-connect-with-windows-authmd"></a>2. &nbsp; [Conecte-se às fontes de dados e aos compartilhamentos de arquivo do Azure locais com a Autenticação do Windows](lift-shift/ssis-azure-connect-with-windows-auth.md)

*Atualizado: 27-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1))

<!-- Source markdown line 66.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 673386fca53cb60b983e0cb3cd4b9e2ee1dee0de 65458b4dceb92d01184c5e9c6f68ec0e8f16ba08  (PR=4104  ,  Filename=ssis-azure-connect-with-windows-auth.md  ,  Dirpath=docs\integration-services\lift-shift\  ,  MergeCommitSha40=19e1c4067142d33e8485cb903a7a9beb7d894015) -->



**Conecte-se ao SQL Server local**

Para verificar se você pode se conectar a um SQL Server local, faça o seguinte:

1.  Para executar este teste, localize um computador não ingressado em domínio.

2.  No computador não ingressado no domínio, execute o seguinte comando para iniciar o SSMS (SQL Server Management Studio) com as credenciais de domínio que você deseja usar:

```
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
```

3.  No SSMS, verifique se você pode se conectar ao SQL Server local que você deseja usar.

**Conecte-se ao compartilhamento de arquivo local**

Para verificar se você pode se conectar a um compartilhamento de arquivos local, faça o seguinte:

1.  Para executar este teste, localize um computador não ingressado em domínio.

2.  No computador não ingressado no domínio, execute o comando a seguir. Este comando abre uma janela de prompt de comando com as credenciais de domínio que você deseja usar e, em seguida, testa a conectividade ao compartilhamento de arquivos obtendo uma listagem de diretórios.

```
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
```

3.  Verifique se a listagem de diretórios é retornada para o compartilhamento de arquivos local que você deseja usar.

**Conecte-se a um compartilhamento de arquivo em uma VM do Azure**

Para se conectar a um compartilhamento de arquivos em uma máquina virtual do Azure, faça o seguinte:

1.  Com o SQL Server Management Studio (SSMS) ou outra ferramenta, conecte-se ao Banco de Dados SQL que hospeda o SSISDB (banco de dados do catálogo do SSIS).

2.  Com o SSISDB como o banco de dados atual, abra uma janela de consulta.

3.  Execute o procedimento armazenado `catalog.set_execution_credential` conforme descrito nas seguintes opções:

```
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
```

**Conecte-se a um compartilhamento de arquivos nos Arquivos do Azure**

Para obter mais informações sobre o Arquivos do Azure, consulte [Arquivos do Azure](https://azure.microsoft.com/services/storage/files/).







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + Atualizado (3 + 14): documentos sobre **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (1 + 0): documentos do **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + Atualizado (87 + 0): documentos sobre **Sistema de Plataforma Analítica para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + Atualizado (5 + 4): documentos sobre **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + Atualizado (0 + 1): documentos sobre o **Mecanismo de Banco de Dados para SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (2 + 2): documentos sobre **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (10 + 9): documentos sobre **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + Atualizado (2 + 4): documentos sobre **Bancos de Dados Relacionais para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (4 + 2): documentos sobre o **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (0 + 1): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + Atualizado (21 + 0): documentos sobre o **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + Atualizado (5 + 1): documentos do **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (0 + 1): documentos do **SSDT (SQL Server Data Tools)**](../ssdt/new-updated-ssdt.md)
- [Novo + Atualizado (1 + 0): documentos sobre o **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 1): documentos do **SSMS (SQL Server Management Studio)**](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (0 + 2): documentos sobre o **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + Atualizado (0 + 0): documentos sobre **DMA (Assistente de Migração de Dados) para o SQL**](../dma/new-updated-dma.md)
- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)


