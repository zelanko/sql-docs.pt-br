---
title: Gerenciador de modelos | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.templates.explorer.f1
- sql13.wb.templates.f1
helpviewer_keywords:
- templates [SQL Server]
- SQL Server Management Studio [SQL Server], Template Explorer
- Template Explorer
- templates [Transact-SQL]
- templates [SQL Server], Template Explorer
ms.assetid: b9ee55c5-bb44-4f76-90ac-792d8d83b4c8
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e0d0525a7da87f0c2f2363d641fcb07bcd5262ad
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="template-explorer"></a>Explorador de Modelos
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] fornece uma variedade de modelos. Modelos são arquivos boilerplate que contêm scripts SQL que ajudam você a criar objetos em um banco de dados. Na primeira vez em que o gerenciador de modelos é aberto, uma cópia dos modelos é colocada na pasta do usuário C:\Users, em AppData\Roaming\Microsoft\SQL Server Management Studio\130\Templates.  
  
Você pode procurar os modelos disponíveis no Gerenciador de Modelos e, depois, abrir um modelo para incorporar o código em uma janela de editor de códigos. Você também pode criar modelos personalizados.  
  
## <a name="benefits-of-templates"></a>Benefícios de modelos  
Os modelos estão disponíveis para soluções, projetos e vários tipos de editores de códigos. Esses modelos estão disponíveis para criar objetos como bancos de dados, tabelas, exibições, índices, procedimentos armazenados, gatilhos, estatísticas e funções. Além disso, há modelos que o ajudam a administrar seu servidor criando propriedades estendidas, servidores vinculados, logons, funções, usuários e modelos para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)].  
  
Os scripts de modelo fornecidos com o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] contêm parâmetros para ajudá-lo a personalizar o código. Quando você abrir um modelo, use a caixa de diálogo **Substituir Parâmetros do Modelo** para inserir valores no script.  
  
Crie modelos personalizados para tarefas executadas com frequência. Organize seus scripts personalizados nas pastas existentes ou crie uma nova estrutura de pastas.  
  
O editor de consultas do [!INCLUDE[ssDE](../../includes/ssde_md.md)] também oferece suporte a trechos de códigos que podem ser inseridos em locais específicos em um script clicando com o botão direito do mouse nesse local.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
Use os tópicos a seguir como introdução rápida a modelos  
  
|**Description**|**Tópico**|  
|-------------------|-------------|  
|Descreve como incorporar o código de um modelo em uma janela de editor de códigos.|[Abrir um modelo](../../ssms/template/open-a-template.md)|  
|Descreve como substituir valores de parâmetros de modelo depois de abrir um modelo em um editor de códigos.|[Substituir Parâmetros do Modelo](../../ssms/template/replace-template-parameters.md)|  
  

