---
title: Caixa de diálogo Alterações Detectadas no Banco de Dados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.schema.databasechangesdetected
- vdtsql.chm:65543
- vdtsql.chm:65554
ms.assetid: 91f13086-371f-46a2-9f46-804c1415f3ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0d5850ce71e483ea33bb99972c243140a63da5f0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63270542"
---
# <a name="database-changes-detected-dialog-box-visual-database-tools"></a>Caixa de diálogo Alterações Detectadas no Banco de Dados (Visual Database Tools)
  Essa caixa de diálogo aparece quando se tenta salvar um diagrama de banco de dados ou tabelas selecionadas, porém, alguns objetos de banco de dados que serão afetados pela ação de gravação encontram-se desatualizados em relação ao banco de dados. Aceitar as alterações mostradas nessa caixa de diálogo atualizará o banco de dados, que poderá corresponder ao diagrama e substituir alterações de outros usuários.  
  
> [!NOTE]  
>  Embora não seja possível desfazer alterações feitas em uma tabela ou diagrama de banco de dados, as alterações não são salvas no banco de dados até que a tabela ou diagrama sejam salvos. Você pode descartar qualquer alteração não salva, selecionando **Não** e fechando todos os diagramas abertos sem os salvar.  
  
## <a name="options"></a>Opções  
 **Aviso sobre detecção de diferença**  
 Determine se essa caixa de diálogo deverá aparecer na próxima vez você tentar salvar um diagrama de banco de dados ou selecionar tabelas. Marcar significa que a caixa de diálogo continuará a aparecer toda vez que você salvar um diagrama ou tabela desatualizados com relação ao banco de dados. Desmarcar significa que a caixa de diálogo não será exibida. Por padrão, essa caixa é marcada. Se desmarcar a opção, você poderá marcá-la novamente na caixa de diálogo **Opções** .  
  
 **Sim**  
 Atualiza o banco de dados com todas as alterações mostradas na lista.  
  
 **Não**  
 Cancela a ação de salvar.  
  
> [!NOTE]  
>  Para atualizar o diagrama de modo que ele corresponda ao banco de dados, feche-o sem salvar as alterações; clique com o botão direito do mouse no diagrama, no Explorador de servidores, e clique em Atualizar. Em seguida, abra novamente o diagrama.  
  
 **Salvar Arquivo de Texto**  
 Exibe a caixa de diálogo **Salvar como** , permitindo especificar um local para um arquivo de texto contendo a lista de alterações do banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Reconciliar um diagrama de banco de dados com um banco de dados modificado &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Ambientes multiusuários &#40;Visual Database Tools&#41;](multiuser-environments-visual-database-tools.md)  
  
  
