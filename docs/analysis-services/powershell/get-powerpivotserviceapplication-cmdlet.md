---
title: "Cmdlet Get-PowerPivotServiceApplication | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 99e4faa1-2f87-43c6-b7ec-a97d4112c5ac
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Cmdlet Get-PowerPivotServiceApplication
  Retorna um ou mais aplicativos de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## Sintaxe  
  
```  
Get-PowerPivotServiceApplication [[-Identity] <SPGeminiServiceApplicationPipeBind>] [<CommonParameters>]  
```  
  
## Description  
 O cmdlet Get-PowerPivotServiceApplication retorna o aplicativo de serviço especificado pelo parâmetro Identity. Se nenhum parâmetro for especificado, o cmdlet retornará todos os aplicativos de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Cada aplicativo é identificado por seu nome para exibição, tipo de aplicativo e GUID. Para exibir as propriedades adicionais de um aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], adicione a opção format-list ao cmdlet.  
  
## Parâmetros  
  
### -Identity \<SPGeminiServiceApplicationPipeBind>  
 Especifica o aplicativo de serviço a ser obtido. O valor deve ser um GUID válido que identifica exclusivamente o objeto no farm.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### \<CommonParameters>  
 Este cmdlet oferece suporte aos parâmetros comuns: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer e OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhum.|  
|Saídas|Nenhum.|  
  
## Exemplo 1  
  
```  
C:\PS>Get-PowerPivotServiceApplication  
```  
  
 Este exemplo retorna um ou mais aplicativos de serviço no farm.  
  
## Exemplo 2  
  
```  
C:\PS>Get-PowerPivotServiceApplication | format-list  
```  
  
 Este exemplo retorna todas as propriedades de um aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
## Exemplo 3  
  
```  
C:\PS>get-PowerPivotServiceApplication -Identity 1234567-890a-bcde-fghijklm  
```  
  
 Este exemplo retorna um único aplicativo de serviço, ao mesmo tempo em que mostra o nome para exibição, o tipo de aplicativo e o GUID do aplicativo. Se o nome para exibição for longo, ele será truncado. Use a opção format-list para exibir o nome completo.  
  
  