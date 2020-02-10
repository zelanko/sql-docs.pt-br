---
title: 'Tarefa 12: descobrindo o conhecimento (descoberta de conhecimento) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: dd80a8e6-1e41-4c49-9898-02b1d2505a10
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6dd54475ee63b2f6ef5e1b56b94c11aafd5996ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484679"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>Tarefa 12: Descobrindo a base de dados de conhecimento (descoberta da base de dados de conhecimento)
  Nesta tarefa, você executa a atividade de **descoberta de conhecimento** nos domínios ID do **fornecedor** e nome do **fornecedor** . Neste cenário, o processo de descoberta da base de dados de conhecimento importa basicamente valores desses dois domínios.  
  
 Neste tutorial, você começou a criar a base de dados de conhecimento do zero. Você também pode começar a criar uma base de dados de conhecimento executando uma atividade de descoberta de conhecimento. Quando você clica em **criar uma base de dados de conhecimento** na página principal, o cliente do DQS leva você para uma página com atividade de gerenciamento de **domínio** selecionada para a atividade. Você pode alterar a **atividade** para **descoberta de conhecimento** e, em seguida, na próxima página, você pode criar domínios como parte do processo de descoberta da base de dados de conhecimento. Consulte [executar descoberta da](https://msdn.microsoft.com/library/hh510398.aspx) base de dados de conhecimento para obter mais detalhes.  
  
1.  Na página principal do cliente do DQS, na seção **base de dados de conhecimento recente** , clique na seta para a **direita** ao lado da base de dados de conhecimento **fornecedores** e clique em descoberta de **conhecimento**. Como alternativa, você pode clicar em **abrir base de dados de conhecimento**, selecionar **fornecedores** na **lista de bases de dados de conhecimento**, selecionar descoberta de **conhecimento** como **atividade** e clicar em **Avançar**.  
  
     ![Menu Descoberta da Base de Dados de Conhecimento na página principal](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "Menu Descoberta da Base de Dados de Conhecimento na página principal")  
  
2.  Selecione o **arquivo do Excel** para a fonte de **dados**.  
  
3.  Clique em **procurar**, navegue e selecione **suppliers. xls**e clique em **abrir**.  
  
4.  Selecione **fornecedores para descoberta** da **planilha**.  
  
5.  Na seção **mapeamentos** , mapeie a coluna **CódigoDoFornecedor** do arquivo do **Excel** para a coluna **nome** do fornecedor e domínio da **ID** do fornecedor para o domínio **nome do fornecedor** usando **listas suspensas**. O arquivo do Excel tem dados de exemplo para os domínios **ID do fornecedor** e **nome do fornecedor** . No processo de descoberta, você pode selecionar os domínios cujos valores você deseja descobrir. Você pode criar domínios nesta página e, depois, mapear as colunas de origem para esses domínios. É comum criar domínios durante a atividade de descoberta da base de dados de conhecimento, em vez de criar domínios durante a atividade de gerenciamento de domínio.  
  
     ![Página Mapa do Processo de Descoberta](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "Página Mapa do Processo de Descoberta")  
  
6.  Clique em **Avançar** para alternar para a página de **descoberta** .  
  
7.  Na página **descobrir** , clique em **Iniciar** para iniciar o processo de descoberta. A descoberta é executada nas colunas **CódigoDoFornecedor** e **nome do fornecedor** no arquivo **suppliers. xls** . Os domínios **ID do fornecedor** e nome do **fornecedor** devem ser preenchidos com o conhecimento desenhado da descoberta.  
  
     ![Página Descoberta do Processo de Descoberta](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "Página Descoberta do Processo de Descoberta")  
  
8.  Após a conclusão da análise, examine as **Estatísticas de origem** na **guia criador de perfil** na parte inferior da página. Observe que foram descobertos 10 novos registros com o total de 20 valores (**CódigoDoFornecedor** e valores de **nome de fornecedor** da **planilha do Excel**). Você também verá quantos valores são: novos; exclusivos; novos e exclusivos; e válidos. Na caixa de listagem à direita, você poderá ver mais detalhes de cada domínio envolvido no processo de descoberta. Se você passar o mouse sobre a barra de status na coluna Integridade, poderá ver se há algum valor ausente nas colunas na fonte.  
  
     ![Resultados da Descoberta da Base de Dados de Conhecimento](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "Resultados da Descoberta da Base de Dados de Conhecimento")  
  
9. Clique em **Avançar** para alternar para a página **gerenciar valores de domínio** .  
  
10. Na página **gerenciar valores de domínio** , clique em domínio **nome do fornecedor** na lista de domínios.  
  
11. No painel direito, clique com o botão direito do mouse em **país lento Storex** (Observe ' x ' no final) e selecione **loja de país lento**. O DQS sugere essa alteração após a execução do verificador ortográfico no domínio. Por padrão, o verificador ortográfico é habilitado nos domínios que você cria.  
  
     ![Nome correto do fornecedor - Lazy Country Store](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "Nome correto do fornecedor - Lazy Country Store")  
  
12. Na lista valores de domínio, confirme se o valor **Storex de país lento** está definido como um erro (marca **X** vermelha) com o **repositório de país lento** como a correção e também o **repositório de país lento** também é adicionado como um valor válido.  
  
     ![Valor do Domínio e Corrigir para Valor](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "Valor do Domínio e Corrigir para Valor")  
  
13. Clique em **Concluir**.  
  
14. Na caixa de diálogo **SQL Server Data Quality Services** , clique em **publicar**.  
  
15. Clique em **OK** na caixa de mensagem de êxito.  
  
     Você concluiu a primeira lição do tutorial.  
  
## <a name="next-step"></a>Próxima etapa  
 [Lição 2: Limpando dados de fornecedor usando a base de dados de conhecimento de fornecedores](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  
