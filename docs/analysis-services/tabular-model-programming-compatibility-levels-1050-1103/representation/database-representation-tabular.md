---
title: Representação de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 16a233fb-f83b-4ca1-acb5-6186eca0a62c
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4c64a2963cf4011e8bb98cb23b6530fc2e3a4c81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="database-representationtabular"></a>Representação de banco de dados (de tabela)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  No modo de tabela, o banco de dados é o contêiner para todos os objetos no modelo de tabela.  
  
## <a name="database-representation"></a>Representação de banco de dados  
 O banco de dados é o local onde residem todos os objetos que constituem um modelo de tabela. O desenvolvedor localiza no banco de dados objetos como conexões, tabelas, funções e muito mais.  
  
### <a name="database-in-amo"></a>Banco de dados no AMO  
 Ao usar o AMO para gerenciar um banco de dados modelo de tabela, o objeto <xref:Microsoft.AnalysisServices.Database> no AMO coincide um-para-um ao objeto lógico de banco de dados em um modelo de tabela.  
  
> [!NOTE]  
>  Para obter acesso a um objeto de banco de dados, no AMO, o usuário precisa ter acesso a um objeto de servidor e conectar-se a ele.  
  
### <a name="database-in-adomdnet"></a>Banco de dados no ADOMD.Net  
 Ao usar o ADOMD para consultar um banco de dados modelo de tabela, a conexão com um banco de dados específico é obtida por meio do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
 Você pode se conectar diretamente a determinado banco de dados usando o seguinte trecho de código:  
  
```csharp  
using ADOMD = Microsoft.AnalysisServices.AdomdClient;  
…  
   ADOMD.AdomdConnection currrentCnx = new ADOMD.AdomdConnection("Data Source=<<server\instance>>;Catalog=<<database>>");  
   currrentCnx.Open();  
…  
  
```  
  
 Além disso, em um objeto de conexão existente (que não foi fechado), você pode alterar o banco de dados atual para outro, conforme mostrado no seguinte trecho de código:  
  
```csharp  
currentCnx.ChangeDatabase("myOtherDatabase");  
  
```  
  
## <a name="database-in-amo"></a>Banco de dados no AMO  
 Ao usar o AMO para gerenciar um objeto de banco de dados, comece com um objeto <xref:Microsoft.AnalysisServices.Server>. Em seguida, procure seu banco de dados na coleção de banco de dados ou crie um novo banco de dados adicionando um à coleção.  
  
 O trecho de código a seguir mostra as etapas para conectar-se a um servidor e criar um banco de dados vazio, depois de verificar que o banco de dados não existe:  
  
```  
  
AMO.Server CurrentServer = new AMO.Server();  
try  
{  
    CurrentServer.Connect(currentServerName);  
}  
catch (Exception cnxException)  
{  
    MessageBox.Show(string.Format("Error while trying to connect to server: [{0}]\nError message: {1}", currentServerName, cnxException.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    return;  
}  
newDatabaseName = DatabaseName.Text;  
if (CurrentServer.Databases.Contains(newDatabaseName))  
{  
    return;  
}  
try  
{  
    AMO.Database newDatabase = CurrentServer.Databases.Add(newDatabaseName);  
  
    CurrentServer.Update();  
}  
catch (Exception createDBxc)  
{  
    MessageBox.Show(String.Format("Database [{0}] couldn't be created.\n{1}", newDatabaseName, createDBxc.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    newDatabaseAvailable = false;  
}  
  
```  
  
 Para obter um entendimento prático de como usar o AMO para criar e manipular representações de banco de dados, consulte o código-fonte no exemplo do Tabular AMO 2012; Verifique especificamente o seguinte arquivo de origem: Database.cs. O exemplo está disponível no Codeplex. O código de exemplo é fornecido apenas como um suporte aos conceitos lógicos explicados aqui e não deve ser usado em um ambiente de produção.  
  
  
