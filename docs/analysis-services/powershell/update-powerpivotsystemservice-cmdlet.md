---
title: "Cmdlet Update-PowerPivotSystemService | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: a90f1158-68d3-4330-98c1-fb0f81e13328
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 8
---
# Cmdlet Update-PowerPivotSystemService
  Atualiza o objeto pai do Serviço de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm.  
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## Sintaxe  
  
```  
Update-PowerPivotSystemService [-Confirm <switch>] [<CommonParameters>]  
```  
  
## Description  
 O cmdlet **Update-PowerPivotSystemService** executa uma série de ações de atualização no objeto pai do Serviço de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], nas instâncias e nos aplicativos de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Todos os serviços da camada intermediária e aplicativos em uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint devem ser executados no mesmo nível funcional. Este cmdlet executa as ações de atualização em todos esses objetos.  
  
 Execute esse cmdlet após a execução da Instalação do SQL Server para instalar uma versão mais nova do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint ou se você tiver aplicado uma atualização cumulativa no servidor. Para verificar se a atualização é necessária, execute `Get-PowerPivotSystemService` para analisar a propriedade **NeedsUpgrade** . Se **NeedsUpgrade** for true, você deverá executar o cmdlet para atualizar os objetos da camada intermediária do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm.  
  
 Como uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint inclui serviços de dados da camada intermediária e de back-end, você deve executar **Update-PowerPivotEngineService** sempre que executar **Update-PowerPivotSystemService** para assegurar que ambas as camadas tenham a mesma versão no farm.  
  
 Não é possível reverter a atualização para a versão anterior. Se você reverter para uma versão anterior, remova o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do seu farm do SharePoint e reinstale o software. Para verificar se a operação de atualização foi bem-sucedida, execute `Get-PowerPivotSystemService` para analisar as propriedades globais das informações de versão e para verificar se **NeedsUpgrade** não está mais definida como true.  
  
## Parâmetros  
  
### -Confirm \<switch>  
 Solicita sua confirmação antes de executar o comando. Este valor é habilitado por padrão. Para ignorar a resposta de confirmação em um comando, especifique Confirm:$false no comando.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### \<CommonParameters>  
 Este cmdlet oferece suporte aos seguintes parâmetros:  
  
-   detalhado  
  
-   Depurador  
  
-   ErrorAction  
  
-   ErrorVariable  
  
-   WarningAction  
  
-   WarningVariable  
  
-   OutBuffer  
  
-   OutVariable  
  
 Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhum.|  
|Saídas|Nenhum.|  
  
  