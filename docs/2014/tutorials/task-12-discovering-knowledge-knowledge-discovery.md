---
title: 'Tarefa 12: Descobrindo os dados de Conhecimento (descoberta de Conhecimento) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: dd80a8e6-1e41-4c49-9898-02b1d2505a10
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d38af78e59a88e05fe874e4b4748b1f6f8b5049c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167696"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>Tarefa 12: Descobrindo a base de dados de conhecimento (descoberta da base de dados de conhecimento)
  Nesta tarefa, você deve executar o **descoberta de Conhecimento** atividade nos **Supplier ID** e **Supplier Name** domínios. Neste cenário, o processo de descoberta da base de dados de conhecimento importa basicamente valores desses dois domínios.  
  
 Neste tutorial, você começou a criar a base de dados de conhecimento do zero. Você também pode começar a criar uma base de dados de conhecimento executando uma atividade de descoberta de conhecimento. Quando você clica em **criar uma Base de dados de Conhecimento** na página principal, cliente DQS levará você para uma página com **gerenciamento de domínio** atividade selecionada para a atividade. Você pode alterar o **atividade** à **descoberta de Conhecimento** e, em seguida, na próxima página você pode criar domínios como parte do processo de descoberta de Conhecimento. Ver [Perform Knowledge Discovery](http://msdn.microsoft.com/library/hh510398.aspx) para obter mais detalhes.  
  
1.  Na página principal do cliente do DQS no **Base de dados de conhecimento recente** seção, clique em **seta para a direita** lado a **fornecedores** da Base de dados de conhecimento e clique em **dados de Conhecimento Descoberta**. Como alternativa, você pode clicar **abrir Base de dados de Conhecimento**, selecione **fornecedores** do **lista de bases de dados de Conhecimento**, selecione **descoberta de Conhecimento**como **atividade** e clique em **próxima**.  
  
     ![Menu de descoberta de Conhecimento na principal página](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "Menu de descoberta de Conhecimento na principal página")  
  
2.  Selecione **arquivo do Excel** para **fonte de dados**.  
  
3.  Clique em **navegue**, navegue e selecione **Suppliers**e clique em **abrir**.  
  
4.  Selecione **fornecedores para descoberta** para **planilha**.  
  
5.  No **mapeamentos** seção, mapeie **SupplierID** coluna a partir o **Excel** o arquivo para o **Supplier ID** domínio e  **Nome do fornecedor** coluna para o **Supplier Name** domínio usando **listas suspensas**. O arquivo do Excel tem dados de exemplo para o **Supplier ID** e **Supplier Name** domínios. No processo de descoberta, você pode selecionar os domínios cujos valores você deseja descobrir. Você pode criar domínios nesta página e, depois, mapear as colunas de origem para esses domínios. É comum criar domínios durante a atividade de descoberta da base de dados de conhecimento, em vez de criar domínios durante a atividade de gerenciamento de domínio.  
  
     ![Página do processo de descoberta de mapa](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "mapear a página do processo de descoberta")  
  
6.  Clique em **próxima** para alternar para o **Discover** página.  
  
7.  Sobre o **Discover** , clique em **iniciar** para iniciar o processo de descoberta. Descoberta é executada nas colunas **SupplierID** e **Supplier Name** no **Suppliers** arquivo. O **Supplier ID** e **Supplier Name** domínios devem ser preenchidos com o conhecimento extraído da descoberta.  
  
     ![Descobrir a página do processo de descoberta](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "descobrir a página do processo de descoberta")  
  
8.  Depois que a análise for concluída, examine os **estatísticas de origem** na **guia Profiler** na parte inferior da página. Observe que 10 novos registros com total de 20 valores (**SupplierID** e **Supplier Name** os valores do **planilha do Excel**) foram descobertos. Você também verá quantos valores são: novos; exclusivos; novos e exclusivos; e válidos. Na caixa de listagem à direita, você poderá ver mais detalhes de cada domínio envolvido no processo de descoberta. Se você passar o mouse sobre a barra de status na coluna Integridade, poderá ver se há algum valor ausente nas colunas na fonte.  
  
     ![Os resultados de descoberta de Conhecimento](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "os resultados de descoberta de Conhecimento")  
  
9. Clique em **próxima** para alternar para o **gerenciar valores de domínio** página.  
  
10. No **gerenciar valores de domínio** , clique em **Supplier Name** domínio na lista de domínios.  
  
11. No painel direito, clique com botão direito **Lazy Country Storex** (Observe o 'x' no final) e selecione **Lazy Country Store**. O DQS sugere essa alteração após a execução do verificador ortográfico no domínio. Por padrão, o verificador ortográfico é habilitado nos domínios que você cria.  
  
     ![Nome correto do fornecedor - Lazy Store de país](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "nome correto do fornecedor - Lazy Store do país")  
  
12. Na lista de valores de domínio, confirme se o valor **Lazy Country Storex** é definido como um erro (vermelho **X** marcar) com **Lazy Country Store** como a correção e também o **Lazy Country Store** também é adicionado como um valor válido.  
  
     ![Domínio de valor e corrigir para valor](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "domínio valor e corrigir para valor")  
  
13. Clique em **Concluir**.  
  
14. Na **SQL Server Data Quality Services** caixa de diálogo, clique em **publicar**.  
  
15. Clique em **Okey** na caixa de mensagem de êxito.  
  
     Você concluiu a primeira lição do tutorial.  
  
## <a name="next-step"></a>Próxima etapa  
 [Lição 2: Limpando dados de fornecedor usando a base de dados de conhecimento de fornecedores](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  
