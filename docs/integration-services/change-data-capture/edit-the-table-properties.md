---
title: Editar as propriedades da tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- editTabProps
ms.assetid: 95ea72ba-8e40-4177-a963-0fb4d10c56e3
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 68e40d458f7a09d9fb073a9771aaeb9b80c6a06c
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35332850"
---
# <a name="edit-the-table-properties"></a>Editar as propriedades da tabela
  Use esta caixa de diálogo para editar as colunas específicas da tabela selecionada onde as alterações estão sendo capturadas. Você também pode editar as informações de **Função de Segurança** e **Instância de Captura** .  
  
### <a name="to-edit-the-columns-to-include-in-the-cdc-instance"></a>Para editar as colunas a serem incluídas na instância CDC  
  
1.  Siga um ou ambos destes procedimentos:  
  
    -   Marque a caixa de seleção ao lado de qualquer coluna adicional que você quer incluir.  
  
    -   Desmarque a caixa de seleção ao lado de qualquer coluna que você não quer mais incluir.  
  
### <a name="to-edit-the-security-role"></a>Para editar a função de segurança  
  
1.  Digite um novo nome ou edite o nome da função de segurança no campo **Função de Segurança** .  
  
### <a name="to-create-a-new-capture-instance"></a>Para criar uma nova instância de captura  
  
1.  Na seção **Função de Segurança** , no campo **Nome** , insira um nome para a instância de captura. Por padrão, o nome inserido no campo é o nome da instância de captura atual com **_NEW** no final do nome (por exemplo, **instância_antiga_NEW**).  
  
2.  Salve a instância de captura como um dos seguintes:  
  
    -   **Nova Instância de Captura**: neste caso, uma nova instância de captura é salva e a instância de captura antiga não é excluída.  
  
         **Observação**: você não pode ter mais que duas instâncias de captura por tabela. Se já houver duas instâncias de captura, esta opção não estará disponível.  
  
    -   **Substituir Existente**: neste caso, a instância de captura atual é excluída e é substituída pela instância de captura criada. Se houver duas instâncias de captura definidas para esta tabela, você deverá selecionar uma para substituir.  
  
 **Observação**: você pode remover uma instância de captura da lista de tabelas na guia **Tabela** .  
  
 Depois de terminar de inserir as informações nesta caixa de diálogo, clique em **OK** para aceitar as alterações.  
  
## <a name="see-also"></a>Consulte Também  
 [Como editar as propriedades de instância CDC](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Fazer alterações nas tabelas selecionadas para capturar alterações](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md)  
  
  
