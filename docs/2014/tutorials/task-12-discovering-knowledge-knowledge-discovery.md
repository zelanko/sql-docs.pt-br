---
title: 'Tarefa 12: Descobrindo a base (de Conhecimento descoberta) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dd80a8e6-1e41-4c49-9898-02b1d2505a10
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b608a384e5281134ae951fdfeca0e89234c4a32a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020161"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>Tarefa 12: Descobrindo a base de dados de conhecimento (descoberta da base de dados de conhecimento)
  Nesta tarefa, você deve executar o **descoberta de Conhecimento** atividade em **Supplier ID** e **Supplier Name** domínios. Neste cenário, o processo de descoberta da base de dados de conhecimento importa basicamente valores desses dois domínios.  
  
 Neste tutorial, você começou a criar a base de dados de conhecimento do zero. Você também pode começar a criar uma base de dados de conhecimento executando uma atividade de descoberta de conhecimento. Quando você clica em **criar uma Base de dados de Conhecimento** na página principal, o cliente DQS levará você até uma página com **gerenciamento de domínio** atividade selecionada para a atividade. Você pode alterar o **atividade** para **descoberta de Conhecimento** e, em seguida, na próxima página você pode criar domínios como parte do processo de descoberta de Conhecimento. Consulte [Executar descoberta de Conhecimento](http://msdn.microsoft.com/library/hh510398.aspx) para obter mais detalhes.  
  
1.  Na página principal do cliente do DQS no **da Base de conhecimento recente** seção, clique em **seta para a direita** lado a **fornecedores** da Base de dados de conhecimento e clique em **conhecimento Descoberta**. Como alternativa, você pode clicar em **abrir Base de dados de Conhecimento**, selecione **fornecedores** do **lista de bases de dados de Conhecimento**, selecione **descoberta de Conhecimento**como **atividade** e clique em **próximo**.  
  
     ![Menu de descoberta de Conhecimento na principal página](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "Menu de descoberta de Conhecimento na principal página")  
  
2.  Selecione **arquivo do Excel** para **fonte de dados**.  
  
3.  Clique em **procurar**, navegue e selecione **Suppliers.xls**e clique em **abrir**.  
  
4.  Selecione **fornecedores para descoberta** para **planilha**.  
  
5.  No **mapeamentos** seção, mapeie **SupplierID** coluna a partir o **Excel** o arquivo para o **Supplier ID** domínio e  **Nome do fornecedor** coluna para o **Supplier Name** domínio usando **listas suspensas**. O arquivo do Excel tem dados de exemplo para o **Supplier ID** e **Supplier Name** domínios. No processo de descoberta, você pode selecionar os domínios cujos valores você deseja descobrir. Você pode criar domínios nesta página e, depois, mapear as colunas de origem para esses domínios. É comum criar domínios durante a atividade de descoberta da base de dados de conhecimento, em vez de criar domínios durante a atividade de gerenciamento de domínio.  
  
     ![Página do processo de descoberta de mapa](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "página do processo de descoberta de mapa")  
  
6.  Clique em **próximo** para alternar para o **Discover** página.  
  
7.  Sobre o **Discover** , clique em **iniciar** para iniciar o processo de descoberta. Descoberta é executada nas colunas **SupplierID** e **Supplier Name** no **Suppliers.xls** arquivo. O **Supplier ID** e **Supplier Name** domínios devem ser preenchidos com o conhecimento extraído da descoberta.  
  
     ![Página do processo de descoberta de descobrir](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "descobrir a página do processo de descoberta")  
  
8.  Depois que a análise for concluída, examine o **estatísticas de origem** no **guia criador de perfil** na parte inferior da página. Observe que 10 novos registros com total de 20 valores (**SupplierID** e **Supplier Name** os valores do **planilha do Excel**) foram descobertos. Você também verá quantos valores são: novos; exclusivos; novos e exclusivos; e válidos. Na caixa de listagem à direita, você poderá ver mais detalhes de cada domínio envolvido no processo de descoberta. Se você passar o mouse sobre a barra de status na coluna Integridade, poderá ver se há algum valor ausente nas colunas na fonte.  
  
     ![Resultados da descoberta de Conhecimento](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "resultados de descoberta de Conhecimento")  
  
9. Clique em **próximo** para alternar para o **gerenciar valores de domínio** página.  
  
10. No **gerenciar valores de domínio** , clique em **Supplier Name** domínio na lista de domínios.  
  
11. No painel direito, clique com botão direito **Lazy Country Storex** (Observe 'x' no final) e selecione **Lazy Country Store**. O DQS sugere essa alteração após a execução do verificador ortográfico no domínio. Por padrão, o verificador ortográfico é habilitado nos domínios que você cria.  
  
     ![Corrija o nome do fornecedor - Lazy Country Store](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "nome correto do fornecedor - Lazy Country Store")  
  
12. Na lista de valores de domínio, confirme se o valor **Lazy Country Storex** é definido como um erro (vermelho **X** marcar) com **Lazy Country Store** como a correção e também o **Lazy Country Store** também é adicionado como um valor válido.  
  
     ![Domínio de valor e corrigir para valor](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "domínio valor e corrigir para valor")  
  
13. Clique em **Concluir**.  
  
14. Em **serviços de qualidade de dados do SQL Server** caixa de diálogo, clique em **publicar**.  
  
15. Clique em **Okey** na caixa de mensagem de êxito.  
  
     Você concluiu a primeira lição do tutorial.  
  
## <a name="next-step"></a>Próxima etapa  
 [Lição 2: Limpando dados de fornecedor usando a base de dados de conhecimento de fornecedores](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  