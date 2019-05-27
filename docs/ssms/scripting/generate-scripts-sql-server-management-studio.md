---
title: Gerar scripts (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: mathoma
ms.topic: conceptual
ms.assetid: 9711c617-3c68-4e5a-aea3-befc64d51524
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 63c772e9957a180b76949ecc95a95661a4632aff
ms.sourcegitcommit: c29150492383f48ef484fa02a483cde1cbc68aca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65820874"
---
# <a name="generate-scripts-sql-server-management-studio"></a>Gerar scripts (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece dois mecanismos para gerar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] . Crie scripts para vários objetos usando o **Assistente para Gerar e Publicar Scripts**. É possível gerar um script para objetos individuais ou para vários objetos usando o menu **Gerar script como** no **Pesquisador de Objetos**.  

Para obter um Tutorial detalhado sobre a criação de script de vários objetos usando o SSMS (SQL Server Management Studio), consulte o [Tutorial: criando scripts no SSMS](https://docs.microsoft.com/sql/ssms/tutorials/scripting-ssms).

  
## <a name="before-you-begin"></a>Antes de começar  
 Escolha o mecanismo que melhor satisfaz seus requisitos.  
  
###  <a name="GenPubScriptWiz"></a> Assistente para Gerar e Publicar Scripts  
 Use o **Assistente para Gerar e Publicar Scripts** para criar um script [!INCLUDE[tsql](../../includes/tsql-md.md)] para vários objetos. O assistente gera um script de todos os objetos de um banco de dados ou de um subconjunto dos objetos selecionado. O assistente tem muitas opções para seus scripts, por exemplo, se permissões, ordenações, restrições etc. devem ser incluídos. Para obter instruções sobre como usar o assistente, veja [Assistente para Gerar e Publicar Scripts](../../relational-databases/scripting/generate-and-publish-scripts-wizard.md).  
  
###  <a name="OEScriptAsMenu"></a> Menu Script Como do Pesquisador de Objetos  
 Use o menu **Gerar Script como do Pesquisador de Objetos** para gerar o script de um único objeto, de vários objetos ou de várias instruções para um único objeto. É possível escolher um de vários tipos de scripts. Por exemplo, para criar, alterar ou descartar o objeto. É possível salvar o script em uma janela do Editor de Consultas em um arquivo ou na Área de Transferência. O script é criado em formato Unicode.  
  
##  <a name="ScriptSingleObject"></a> Para gerar um script de um único objeto  
 **Para gerar script de um único objeto**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**e o banco de dados que contém o objeto do qual será gerado um script.  
  
3.  Expanda a categoria do objeto. Por exemplo, expanda o nó **Tabelas** ou **Exibições** .  
  
4.  Clique com o botão direito do mouse no objeto, aponte para **Script \<object type> como**, por exemplo, aponte para **Tabela de Script como**.  
  
5.  Aponte para o tipo de script, como **Criar para** ou **Alterar para**.  
  
6.  Selecione o local para salvar o script, como **Nova janela do Editor de Consultas** ou **Área de Transferência**.  

    ![Tabela de script](media/generate-scripts-sql-server-management-studio/scripttable.png)
  
  
 Use o painel **Detalhes do Pesquisador de Objetos** para gerar um script para vários objetos da mesma categoria.  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**e o banco de dados que contém os objetos dos quais será gerado um script.  
  
3.  Expanda o nó de categoria dos tipos de objeto dos quais você deseja gerar o script, como o nó **Tabelas** .  
  
4.  Abra o painel **Detalhes do Pesquisador de Objetos** selecionando **F7**ou abrindo o menu **Exibição** e selecionando **Detalhes do Pesquisador de Objetos**.  
  
5.  Clique com o botão esquerdo do mouse em um dos objetos dos quais você deseja gerar um script.  
  
6.  Clique em Ctrl + botão esquerdo do mouse no segundo objeto do qual você deseja gerar um script.  
  
7.  Clique com o botão direito do mouse em um dos objetos selecionados e selecione **Script \<object type> como**.  

    ![Pesquisador de Objetos](media/generate-scripts-sql-server-management-studio/objectexplorerdetails.png)
  
  
