---
title: "Cmdlet New-PowerPivotSystemServiceInstance | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 7ea94113-c0f1-4cca-9228-f1a034fba5db
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Cmdlet New-PowerPivotSystemServiceInstance
  Adiciona uma nova instância do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a um servidor de aplicativos.  
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## Sintaxe  
  
```  
New-PowerPivotSystemServiceInstance [[-ParentService] <PowerPivotMidTierServicePipeBind>] [-SystemServiceInstanceName <string>] [-Provision] [<CommonParameters>]  
```  
  
## Description  
 O cmdlet New-PowerPivotSystemServiceInstance provisiona um novo objeto PowerPivotSystemService no nível do farm após o uso da Instalação do SQL Server para instalar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no servidor de aplicativos local. Somente é possível provisionar uma instância de serviço em cada servidor de aplicativos.  Se o serviço já foi provisionado, você não poderá executar esse cmdlet.  
  
## Parâmetros  
  
### -ParentService <PowerPivotMidTierServicePipeBind>\>  
 Especifica o GUID do objeto pai do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Nesta versão, apenas um objeto pai é permitido. Você pode usar Get-PowerPivotSystemService para retornar o objeto de serviço ou seu GUID.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### -SystemServiceInstanceName \<string>  
 Especifica um nome que identifica esse objeto.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### Provision [\<SwitchParameter>]  
 Torna o serviço disponível no SharePoint. Os valores válidos são $true ou $false.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
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
C:\PS>New-PowerPivotSystemServiceInstance -Provision:$true  
```  
  
 Este exemplo mostra o formulário mais comum do cmdlet. Ele registra o Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no servidor de aplicativos local com o farm.  
  
## Exemplo 2  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -SystemServiceInstanceName "MyPSSInstance" -provision:$false  
```  
  
 Este exemplo denomina a instância do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], mas sem provisioná-la. Se você não fornecer um nome, o nome padrão Instância de Serviço de Sistema do SQL Server Analysis Services será usado. A criação de um nome personalizado para o serviço é opcional. Você poderá atribuir um nome ao serviço para oferecer suporte a cenários de teste ou se tiver uma ferramenta ou um script personalizado que provisione a instância em uma etapa posterior.  
  
  