---
title: 'Etapa 1: copiar o pacote da Lição 5 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a1c1887e7229d0e63028c4da09e933dea1dffc0c
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35408938"
---
# <a name="lesson-6-1---copying-the-lesson-5-package"></a>Lição 6-1 – copiar o pacote da Lição 5
Nesta tarefa, você criará uma cópia do pacote Lesson 5.dtsx criado na lição 5. Como alternativa, é possível adicionar o pacote concluído da Lição 5 incluído com o tutorial do projeto e copiá-lo. Você usará esta cópia nova ao longo de toda a lição 6.  
  
### <a name="to-copy-the-lesson-5-package"></a>Para copiar o pacote da Lição 5  
  
1.  Se o SQL Server Data Tools ainda não estiver aberto, clique em Iniciar, aponte para Todos os Programas, aponte para Microsoft SQL Server 2012 e clique em SQL Server Data Tools.  
  
2.  No menu Arquivo, clique em Abrir, clique em Projeto/Solução, selecione Tutorial do SSIS, clique em Abrir e clique duas vezes em SSIS Tutorial.sln.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse em Lesson 5.dtsx e, em seguida, clique em Copiar.  
  
4.  No Gerenciador de Soluções, clique com o botão direito do mouse em Pacotes SSIS e clique em Colar.  
  
    Por padrão, o pacote copiado recebe o nome de Lesson 6.dtsx.  
  
5.  No Gerenciador de Soluções, clique duas vezes em Lesson 6.dtsx para abrir o pacote.  
  
6.  Clique com o botão direito do mouse em qualquer local do plano de fundo da guia Fluxo de Controle e clique em Propriedades.  
  
7.  Na janela Propriedades, atualize a propriedade de Nome da lição 6.  
  
8.  Clique na caixa da propriedade ID, clique na seta suspensa e em <Generate New ID>.  
  
### <a name="to-add-the-completed-lesson-5-package"></a>Para adicionar o pacote concluído da lição 5  
  
1.  Abra o SQL Server Data Tools e abra o projeto do Tutorial do SSIS.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse em Pacotes SSIS e clique em Adicionar Pacote Existente.  
  
3.  Na caixa de diálogo Adicionar Cópia do Pacote Existente, em Local do Pacote, selecione Sistema de Arquivos.  
  
4.  Clique no botão Procurar (...), Lesson 5.dtsx no computador e clique em **Abrir**.  
  
    Para baixar todos os pacotes de lição para este tutorial, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **DOWNLOADS** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie e cole o pacote da Lição 5 conforme descrito nas etapas de 3 a 8 do procedimento anterior.  
  
    Depois de copiar o pacote da lição 5, se você tiver atualmente os pacotes das lições anteriores em sua solução, clique com o botão direito do mouse em cada pacote das lições de 1 a 5 e clique em Excluir do Projeto. Ao terminar, você deve ter apenas a Lição 6.dtsx em sua solução.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Etapa 2: Convertendo o projeto para o modelo de implantação de projetos](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
