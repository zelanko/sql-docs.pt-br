---
title: Localizar a versão do esquema de definição de relatório | Microsoft Docs
description: Saiba como identificar a versão do esquema RDL (Report Definition Language) do seu arquivo de definição de relatório.
ms.date: 06/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- XML schemas [Reporting Services]
- Report Definition Language, XML schema
- schemas [Reporting Services]
ms.assetid: 67954419-1b61-4481-a3b9-23b4ba7a5624
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fd43fb3dba83ab3821b1b670468e7849faac2044
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79510137"
---
# <a name="find-the-report-definition-schema-version-ssrs"></a>Localizar a versão do esquema de definição de relatório (SSRS)

Um arquivo de definição de relatório especifica o namespace do RDL para a versão do esquema de definição de relatório usado para validar o arquivo .rdl. Quando você abre um arquivo .rdl em um ambiente de criação de relatório, como o Designer de Relatórios em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], no Visual Studio ou no Construtor de Relatórios. Caso o relatório tenha sido criado para um namespace anterior, um arquivo de backup será criado automaticamente, e o relatório será atualizado para o namespace atual. Se você salvar a definição de relatório atualizada, terá salvo o arquivo .rdl convertido. Esse é o único modo para atualizar uma definição de relatório. A própria definição de relatório não é atualizada em um servidor de relatório. O relatório compilado é atualizado em um servidor de relatório. Para obter mais informações, consulte [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
## <a name="how-to-identify-the-rdl-schema-version-of-a-report"></a>Como fazer: Identificar a versão do esquema RDL de um relatório  
  
1. Abra o arquivo de relatório .rdl em um aplicativo como o Bloco de Notas ou Bloco de Notas XML que permite visualizar o XML.  
  
     O elemento Relatório XML especifica o namespace do esquema. Por exemplo, o elemento Relatório a seguir especifica o namespace do Designer de Relatórios e o namespace da definição de relatório.  
  
    ``` XML 
    <Report xmlns:rd="http://schemas.microsoft.com/SQLServer/reporting/reportdesigner" xmlns="http://schemas.microsoft.com/sqlserver/reporting/2016/01/reportdefinition" xmlns:df="http://schemas.microsoft.com/sqlserver/reporting/2016/01/reportdefinition/defaultfontfamily" MustUnderstand="df">  
    ```  
  
     O namespace de definição de relatório mais recente é 2016. No entanto, o namespace de definição de relatório publicado mais recente é 2010, especificado pela seguinte URL: `https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition`.
  
### <a name="how-to-identify-the-rdl-schema-version-of-report-designer"></a>Como fazer: identificar a versão do esquema RDL de um Designer de Relatórios  
  
1.  Abrir um novo projeto. A versão do projeto que você escolhe determina a versão do esquema RDL. No SQL Server, há suporte para mais de uma versão de esquema. Para obter mais informações, consulte [Implantação e suporte de versão no SQL Server Data Tools](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
2.  No menu **Projeto** , clique em **Adicionar Novo Item**. A caixa de diálogo **Adicionar Novo Item** é aberta.  
  
3.  No painel **Modelos** , clique em **Relatório**.  
  
4.  Em **Nome**, digite um nome para o relatório ou aceite o padrão.  
  
5.  Clique em **Adicionar**. O Designer de Relatórios abre um novo relatório em branco na exibição Design.  
  
6.  No menu **Exibir** , clique em **Código**. A definição de relatório é exibida como um arquivo XML.  
  
    O elemento Relatório XML especifica o namespace do esquema. Por exemplo, o elemento Relatório a seguir especifica o namespace do Designer de Relatórios e o namespace da definição de relatório.  
  
    ``` XML 
    <Report xmlns:rd="http://schemas.microsoft.com/SQLServer/reporting/reportdesigner" xmlns="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" xmlns:df="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition/defaultfontfamily" MustUnderstand="df">  
    ```  
  
     O namespace de definição de relatório é especificado pela seguinte URL: `https://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition`  
  
### <a name="how-to-identify-the-rdl-schema-version-on-the-report-server"></a>Como fazer: identificar a versão do esquema RDL no Servidor de Relatórios  
  
-   No portal da Web, digite a URL para o servidor de relatório. Por exemplo, a URL a seguir especifica um servidor de relatório no computador local:  
  
     `https://localhost/reportserver/reportdefinition.xsd`  
  
     O arquivo .xsd é aberto no navegador.  
  
     O elemento de Esquema XML especifica o namespace do esquema. Por exemplo, o elemento de esquema a seguir especifica três namespaces: a referência targetNamespace que é usada internamente pelo [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], a referência xsd do próprio esquema (xsd) e a referência de definição de relatório.  *Ano* representa o ano do esquema que o relatório está usando. Por exemplo, 2010 ou 2016.
  
    ``` XML  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" targetNamespace="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" elementFormDefault="qualified">  
    ```  
  
     O namespace de definição de relatório é especificado pela seguinte URL: `https://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition`  

## <a name="next-steps"></a>Próximas etapas
[Atualizar relatórios](../../reporting-services/install-windows/upgrade-reports.md)   
[Linguagem RDL](../../reporting-services/reports/report-definition-language-ssrs.md)   

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
