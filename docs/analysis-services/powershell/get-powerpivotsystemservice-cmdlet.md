---
title: "Cmdlet Get-PowerPivotSystemService | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 33231250-3880-4d75-936b-d70662a01855
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Cmdlet Get-PowerPivotSystemService
  Retorna as propriedades globais do objeto do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um farm.  
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## Sintaxe  
  
```  
Get-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [<CommonParameters>]  
```  
  
## Description  
 O cmdlet Get-PowerPivotSystemService retorna as propriedades globais do objeto do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Há um objeto pai por farm, mas cada farm pode ter várias instâncias do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] executadas em servidores de aplicativo individuais no farm. O objeto pai mostra configurações no nível do servidor que não variam por instância. Se o farm incluir várias instalações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, uma lista delimitada por vírgulas das instâncias indicará quantas instâncias do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] estão no farm.  
  
## Parâmetros  
  
### -Identity \<PowerPivotMidTierServicePipeBind>  
 Especifica o objeto pai a ser obtido. O valor deve ser um GUID válido que identifica exclusivamente o objeto no farm.  
  
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
C:\PS>Get-PowerPivotSystemService  
```  
  
 Este exemplo retorna as propriedades globais do objeto pai, mostrando as propriedades que são compartilhadas por todas as instâncias do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm.  
  
  