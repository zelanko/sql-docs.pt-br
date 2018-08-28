---
title: Caixa de diálogo Verificar Restrição (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraint
ms.assetid: ad0bbf7f-b0de-406a-bd0a-cb779816b101
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 11bc7d3077e14c7cc3993b70ddb6be8ff0411f1f
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "42774383"
---
# <a name="check-constraint-dialog-box-visual-database-tools"></a>Caixa de diálogo Verificar Restrição (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Essa caixa de diálogo aparece quando você clica com o botão direito do mouse em uma grade de definição de tabela no Designer de Tabela e clica em **Verificar Restrições**. A caixa de diálogo contém um conjunto de propriedades para restrições não exclusivas anexadas às tabelas em seu banco de dados. As propriedades que se aplicam a restrições exclusivas aparecem na caixa de diálogo **Índices/Chaves** .  
  
> [!NOTE]  
> Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
## <a name="options"></a>Opções  
**Restrições de Verificação Selecionadas**  
Lista as restrições de verificação disponíveis. Para exibir as propriedades de uma restrição, selecione-a na lista.  
  
**Adicionar**  
Cria uma nova restrição para a tabela de banco de dados selecionada e fornece um nome padrão e outros valores para a restrição. A restrição não será válida até que uma expressão é digitada para a restrição.  
  
**Delete (excluir)**  
Remova a restrição selecionada da tabela. Para cancelar a adição de uma restrição de verificação, use esse botão para remover a restrição.  
  
**Categoria Geral**  
Expanda para mostrar o campo de propriedade **Expressão** .  
  
**Expressão**  
Exibe a expressão para a restrição de verificação selecionada. Para nova restrições, você deve digitar a expressão antes de sair dessa caixa. Você também pode editar restrições de verificação existentes. Para obter mais informações, veja [Como trabalhar com restrições (Visual Database Tools)](http://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e).  
  
**Categoria de identidade**  
Expanda para mostrar propriedades para **Nome** e **Descrição**.  
  
**Nome**  
Mostra o nome da restrição de verificação selecionada. Para alterar o nome dessa restrição, digite o texto diretamente no campo de propriedade.  
  
**Descrição**  
Descrevendo a restrição de verificação. Você pode editar a descrição, digitando no campo de propriedade ou clicando no botão de reticências (**…**), que aparece à direita do campo de propriedade e editar a descrição na caixa de diálogo **Propriedade de Descrição** .  
  
**Categoria do Designer de Tabelas**  
Expanda para mostrar as propriedades de **Verificar Dados Existentes ao Criar ou Habilitar Novamente**, **Impor para Inserir e Atualizar**e **Impor Replicação**.  
  
**Check Existing Data On Creation or Re-Enabling**  
Especifica se todos os dados preexistentes (dados existentes na tabela antes de a restrição ser criada) são verificados em relação à restrição.  
  
**Impor para Inserir e Atualizar**  
Especifica se a restrição é imposta quando os dados são inseridos ou atualizados na tabela.  
  
**Impor para Replicação**  
Indica se é para impor a restrição quando um agente de replicação executar uma inserção ou atualização nesta tabela.  
  
## <a name="see-also"></a>Consulte Também  
[Como trabalhar com restrições (Visual Database Tools)](http://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e)  
[Índices – caixa de diálogo Chaves &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/indexes-keys-dialog-box-visual-database-tools.md)  
  
