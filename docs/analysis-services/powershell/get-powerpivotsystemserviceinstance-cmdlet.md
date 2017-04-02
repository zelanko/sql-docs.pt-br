---
title: "Cmdlet Get-PowerPivotSystemServiceInstance | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 56027a8e-1949-4349-b616-68c8b1d2963c
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Cmdlet Get-PowerPivotSystemServiceInstance
  Retorna uma ou mais instâncias do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em execução em servidores de aplicativos no farm.  
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## Sintaxe  
  
```  
Get-PowerPivotSystemServiceInstance [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## Description  
 O cmdlet Get-PowerPivotSystemServiceInstance retorna as propriedades de uma ou mais instâncias do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em execução no farm. O cmdlet relata o tipo de aplicativo, o status (online ou offline) e a identidade. Para exibir propriedades adicionais de uma instância específica, adicione o parâmetro Identity e a opção format-list ao cmdlet.  
  
## Parâmetros  
  
### -Identity \<PowerPivotMidTierServiceInstancePipeBind>  
 Especifica a instância de serviço a ser obtida. O valor deve ser um GUID válido que identifica exclusivamente o objeto no farm.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### \<CommonParameters>  
 Este cmdlet oferece suporte aos parâmetros comuns: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer e OutVariable. Para obter mais informações, consulte [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)  
  
## Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhum.|  
|Saídas|Nenhum.|  
  
## Exemplo 1  
  
```  
C:\PS>Get-PowerPivotSystemServiceInstance -Identity 1234567-890a-bcde-fghijklm | format-list| format-list  
```  
  
 Este exemplo retorna propriedades adicionais da instância especificada, incluindo o nome do servidor, a versão e o status de atualização.  
  
  