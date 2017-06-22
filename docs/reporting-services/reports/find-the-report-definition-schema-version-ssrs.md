---
title: "Localizar a versão de esquema de definição de relatório (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML schemas [Reporting Services]
- Report Definition Language, XML schema
- schemas [Reporting Services]
ms.assetid: 67954419-1b61-4481-a3b9-23b4ba7a5624
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 354f69ea0d63502a66db541f968f0efe2e690a6e
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---

# <a name="find-the-report-definition-schema-version-ssrs"></a>Localizar a versão do esquema de definição de relatório (SSRS)

Um arquivo de definição de relatório especifica o namespace do RDL para a versão do esquema de definição de relatório usado para validar o arquivo .rdl. Ao abrir um arquivo .rdl no ambiente de criação de relatório como o Designer de Relatórios do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou Construtor de Relatórios, se o relatório tiver sido criado para um namespace anterior, um arquivo de backup será criado automaticamente e o relatório será atualizado para o namespace atual. Se você salvar a definição de relatório atualizada, terá salvo o arquivo .rdl convertido. Esse é o único modo para atualizar uma definição de relatório. A própria definição de relatório não é atualizada em um servidor de relatório. O relatório compilado é atualizado em um servidor de relatório. Para obter mais informações, consulte [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
### <a name="how-to-identify-the-rdl-schema-version-of-a-report"></a>Como identificar a versão do esquema RDL de um relatório  
  
1.  Abra o arquivo de relatório .rdl em um aplicativo como o Bloco de Notas ou Bloco de Notas XML 2007, que permite visualizar o xml.  
  
     O elemento Relatório XML especifica o namespace do esquema. Por exemplo, o elemento Relatório a seguir especifica o namespace do Designer de Relatórios e o namespace da definição de relatório.  
  
    ```  
    <Report xmlns:rd=http://schemas.microsoft.com/SQLServer/reporting/reportdesigner   
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     O namespace de definição de relatório é especificado pela seguinte URL: `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`.  
  
### <a name="how-to-identify-the-rdl-schema-version-of-report-designer"></a>Como identificar a versão do esquema RDL de um Designer de Relatórios  
  
1.  Abrir um novo projeto. A versão do projeto que você escolhe determina a versão do esquema RDL. No SQL Server, há suporte para mais de uma versão de esquema. Para obter mais informações, consulte [implantação e suporte de versão no SQL Server Data Tools](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
2.  No menu **Projeto** , clique em **Adicionar Novo Item**. A caixa de diálogo **Adicionar Novo Item** é aberta.  
  
3.  No painel **Modelos** , clique em **Relatório**.  
  
4.  Em **Nome**, digite um nome para o relatório ou aceite o padrão.  
  
5.  Clique em **Adicionar**. O Designer de Relatórios abre um novo relatório em branco na exibição Design.  
  
6.  No menu **Exibir** , clique em **Código**. A definição de relatório é exibida como um arquivo XML.  
  
     O elemento Relatório XML especifica o namespace do esquema. Por exemplo, o elemento Relatório a seguir especifica o namespace do Designer de Relatórios e o namespace da definição de relatório.  
  
    ```  
    <Report xmlns:rd=http://schemas.microsoft.com/SQLServer/reporting/reportdesigner  
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     O namespace de definição de relatório é especificado pela seguinte URL: `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  
  
### <a name="how-to-identify-the-rdl-schema-version-on-the-report-server"></a>Como identificar a versão do esquema RDL no Servidor de Relatórios  
  
-   No Gerenciador de Relatórios, digite a URL para o servidor de relatório: Por exemplo, a URL a seguir especifica um servidor de relatório no computador local:  
  
     `http://localhost/reportserver/reportdefinition.xsd`  
  
     O arquivo .xsd é aberto no navegador.  
  
     O elemento de Esquema XML especifica o namespace do esquema. Por exemplo, o elemento de esquema a seguir especifica três namespaces: a referência targetNamespace que é usada internamente pelo [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], a referência xsd do próprio esquema (xsd) e a referência de definição de relatório.  
  
    ```  
    <xsd:schema   
    targetNamespace="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    elementFormDefault="qualified">  
    ```  
  
     O namespace de definição de relatório é especificado pela seguinte URL: `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  

## <a name="next-steps"></a>Próximas etapas

[Atualizar relatórios](../../reporting-services/install-windows/upgrade-reports.md)   
[Linguagem de definição de relatório](../../reporting-services/reports/report-definition-language-ssrs.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
