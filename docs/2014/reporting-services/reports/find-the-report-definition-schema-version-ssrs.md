---
title: Localizar a versão do esquema de definição de relatório (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- XML schemas [Reporting Services]
- Report Definition Language, XML schema
- schemas [Reporting Services]
ms.assetid: 67954419-1b61-4481-a3b9-23b4ba7a5624
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 42fd97141fad21c9995857a6e51c495cf6eac078
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151907"
---
# <a name="find-the-report-definition-schema-version-ssrs"></a>Localizar a versão do esquema de definição de relatório (SSRS)
  Um arquivo de definição de relatório especifica o namespace do RDL para a versão do esquema de definição de relatório usado para validar o arquivo .rdl. Ao abrir um arquivo .rdl no ambiente de criação de relatório como o Designer de Relatórios do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou Construtor de Relatórios, se o relatório tiver sido criado para um namespace anterior, um arquivo de backup será criado automaticamente e o relatório será atualizado para o namespace atual. Se você salvar a definição de relatório atualizada, terá salvo o arquivo .rdl convertido. Esse é o único modo para atualizar uma definição de relatório. A própria definição de relatório não é atualizada em um servidor de relatório. O relatório compilado é atualizado em um servidor de relatório. Para obter mais informações, consulte [Upgrade Reports](../install-windows/upgrade-reports.md).  
  
### <a name="how-to-identify-the-rdl-schema-version-of-a-report"></a>Como identificar a versão do esquema RDL de um relatório  
  
1.  Abra o arquivo de relatório .rdl em um aplicativo como o Bloco de Notas ou Bloco de Notas XML 2007, que permite visualizar o xml.  
  
     O elemento Relatório XML especifica o namespace do esquema. Por exemplo, o elemento Relatório a seguir especifica o namespace do Designer de Relatórios e o namespace da definição de relatório.  
  
    ```  
    <Report xmlns:rd=http://schemas.microsoft.com/SQLServer/reporting/reportdesigner   
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     O namespace de definição de relatório é especificado pela seguinte URL: `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`.  
  
### <a name="how-to-identify-the-rdl-schema-version-of-report-designer"></a>Como identificar a versão do esquema RDL de um Designer de Relatórios  
  
1.  Abrir um novo projeto. A versão do projeto que você escolhe determina a versão do esquema RDL. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], há suporte para mais de uma versão de esquema. Para obter mais informações, veja [Implantação e suporte de versão no SQL Server Data Tools &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
2.  No menu **Projeto**, clique em **Adicionar Novo Item**. A caixa de diálogo **Adicionar Novo Item** é aberta.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Atualizar relatórios](../install-windows/upgrade-reports.md)   
 [Linguagem RDL &#40;SSRS&#41;](report-definition-language-ssrs.md)  
  
  
