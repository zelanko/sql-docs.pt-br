---
title: 'Tarefa 3: importando valores de domínio de um arquivo do Excel | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 242e8309-1195-495b-9cd5-aa127748c185
ms.author: lle
author: lrtoyou1223
ms.openlocfilehash: 36c34be6d994c543eb17f8c923fcf62c0fdd53d4
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177266"
---
# <a name="task-3-importing-domain-values-from-an-excel-file"></a>Tarefa 3: Importando valores de domínio de um arquivo do Excel

  Nesta tarefa, você importará valores para o domínio **State** de uma planilha de um arquivo do Excel.

1.  Clique no domínio **State** na **Lista de domínios**.

2.  Verifique se a guia **Valores de Domínio** está ativa no painel direito.

3.  No painel direito, na barra de ferramentas, clique na **seta para baixo** ao lado do botão **Importar valores** e clique em **Importar Valores Válidos do Excel**.

     ![Importar Valores Válidos do Menu Excel](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-01.jpg "Importar Valores Válidos do Menu Excel")

4.  Clique em **Procurar**, selecione **Suppliers.xls**e clique em **Abrir**.

5.  Selecione **StatesToImport$** em **Planilha**.

     ![Caixa de diálogo Importar Valores do Domínio](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-02.jpg "Caixa de diálogo Importar Valores do Domínio")

6.  Clique em **OK** para fechar a caixa de diálogo **Importar Valores de Domínio** . Você deve visualizar todos os nomes dos estados que importou na lista. Observe que a opção **Mostrar Somente Novo** é selecionada automaticamente após a importação. Quando você importa valores e não vê os valores antigos na lista, isso ocorre porque essa opção é habilitada automaticamente após a importação. Para visualizar todos os valores, desmarque a caixa de seleção. Se você importar o mesmo conjunto de valores novamente, nenhum dos valores será importado, pois já existem no domínio.

     ![Caixa de seleção Mostrar Somente Novos em Valores do Domínio](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-03.jpg "Caixa de seleção Mostrar Somente Novos em Valores do Domínio")

## <a name="next-step"></a>Próxima etapa
 [Tarefa 4: Definindo regras de domínio](../../2014/tutorials/task-4-setting-domain-rules.md)


