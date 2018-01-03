---
title: "Caixa de diálogo Tabelas e Colunas (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vdt.dlgbox.tablesandcolumns
ms.assetid: 8cf27be1-e66d-4735-a428-9ab4b33af4f5
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b828265e9f8e85e240420acd795ed9ab0494e4b4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="tables-and-columns-dialog-box-visual-database-tools"></a>Caixa de dialogo Tabelas e Colunas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Use esta caixa de diálogo para mapear uma chave primária em uma tabela para uma chave estrangeira em outra. Para acessar essa caixa de diálogo, no menu **Designer de Tabela** , clique em **Relações**. Na caixa de diálogo **Relações de Chave Estrangeira** , clique no campo **Especificação das Tabelas e Colunas** e, em seguida, clique nas reticências **(…)** à direita da propriedade.  
  
> [!NOTE]  
> Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
## <a name="options"></a>Opções  
**Nome da Relação**  
Mostra o nome da relação.  
  
**Tabela de Chaves Primárias**  
Lista as tabelas no banco de dados Selecione a tabela que estará no lado da chave primária da relação.  
  
**Tabela de Chaves Estrangeiras**  
Mostra a tabela no lado da chave estrangeira da relação. Essa é a tabela selecionada atualmente no Designer de Tabela.  
  
**Grade abaixo da Tabela de Chaves Primárias**  
Lista as colunas da tabela selecionada na lista da **Tabela de Chaves Primárias** . Insira as colunas que contribuam para a chave primária daquela tabela.  
  
**Grade abaixo da Tabela de Chaves Estrangeiras**  
Lista as colunas da tabela selecionada na lista da **Tabela de Chaves Estrangeiras** . Insira a coluna das chaves estrangeiras da tabela das chaves estrangeiras que corresponde à coluna das chaves primárias.  
  
> [!NOTE]  
> As colunas selecionadas para a chave estrangeira devem ter o mesmo tipo de dados das colunas primárias às quais elas correspondem. Deve haver um número igual de colunas em cada uma das chaves. Por exemplo, se a chave primária da tabela no lado primário da relação estiver composta de duas colunas, será necessário coincidir cada uma dessas colunas com uma coluna na tabela no lado da chave estrangeira da relação.  
  
## <a name="see-also"></a>Consulte Também  
[Como criar relações entre tabelas (Visual Database Tools)](http://msdn.microsoft.com/en-us/867a54b8-5be4-46e6-9702-49ae6dabf67c)  
  
