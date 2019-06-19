---
title: Caixa de diálogo Tabelas e Colunas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.tablesandcolumns
ms.assetid: 8cf27be1-e66d-4735-a428-9ab4b33af4f5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 056c200ec6b73cb7cf11ee4b3acf35bc331110b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204671"
---
# <a name="tables-and-columns-dialog-box-visual-database-tools"></a>Caixa de dialogo Tabelas e Colunas (Visual Database Tools)
  Use esta caixa de diálogo para mapear uma chave primária em uma tabela para uma chave estrangeira em outra. Para acessar essa caixa de diálogo, no menu **Designer de Tabela** , clique em **Relações**. Na caixa de diálogo **Relações de Chave Estrangeira**, clique no campo **Especificação das Tabelas e Colunas** e, em seguida, clique nas reticências **(…)** à direita da propriedade.  
  
> [!NOTE]  
>  Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
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
>  As colunas selecionadas para a chave estrangeira devem ter o mesmo tipo de dados das colunas primárias às quais elas correspondem. Deve haver um número igual de colunas em cada uma das chaves. Por exemplo, se a chave primária da tabela no lado primário da relação estiver composta de duas colunas, será necessário coincidir cada uma dessas colunas com uma coluna na tabela no lado da chave estrangeira da relação.  
  
## <a name="see-also"></a>Consulte também  
 [Criar relações de chaves estrangeiras](../../relational-databases/tables/create-foreign-key-relationships.md)  
  
  
