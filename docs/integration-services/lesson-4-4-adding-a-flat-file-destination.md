---
title: 'Etapa 4: adicionar um destino de arquivo simples | Microsoft Docs'
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
ms.assetid: f4088de3-16d8-419c-96a1-a2cd005d0a5b
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a66649974ee1821388ad362aedb14cfd1d20f1c7
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35400208"
---
# <a name="lesson-4-4---adding-a-flat-file-destination"></a>Lição 4-4 – adicionar um destino de arquivo simples
A saída de erro da transformação Pesquisa de Códigos de Moeda redireciona para a transformação Script todas as linhas de dados que falharam na operação de pesquisa. Para aprimorar as informações sobre os erros que ocorreram, a transformação Script executa um script que adquire a descrição de erros.  
  
Nessa tarefa, você salvará todas essas informações sobre as linhas com falha em um arquivo delimitado, para processamento posterior. Para salvar as linhas com falha, você deve adicionar e configurar um gerenciador de conexões de arquivo simples para o arquivo de texto que conterá os dados de erro e um arquivo simples de destino. Ao definir propriedades no gerenciador de conexões de arquivo simples que o arquivo simples usa, você pode especificar como o destino do arquivo simples formata e escreve o arquivo de texto. Para obter mais informações, consulte [Flat File Connection Manager](../integration-services/connection-manager/flat-file-connection-manager.md) e [Flat File Destination](../integration-services/data-flow/flat-file-destination.md).  
  
### <a name="to-add-and-configure-a-flat-file-destination"></a>Para adicionar e configurar um destino de arquivo simples  
  
1.  Clique na guia **Fluxo de Dados** .  
  
2.  Na **Caixa de Ferramentas do SSIS**, expanda **Outros**e arraste **Destino de Arquivo Simples** para a superfície de design de fluxo de dados. Coloque **Destino de Arquivo Simples** diretamente embaixo da transformação **Obter Descrição do Erro** .  
  
3.  Clique na transformação **Obter Descrição do Erro** e arraste a seta verde sobre o novo **Destino de Arquivo Simples**.  
  
4.  Na superfície de design de **Fluxo de Dados** , clique em **Destino de Arquivo Simples** , na recém-adicionada transformação **Destino de Arquivo Simples** , e altere o nome para **Linhas com Falha**.  
  
5.  Clique com o botão direito do mouse na transformação **Linhas com Falha** , clique em **Editar**e, no **Editor de Destino de Arquivo Simples**, clique em **Novo**.  
  
6.  Na caixa de diálogo **Formato de Arquivo Simples** , verifique se **Delimitado** está selecionado e depois clique em **OK**.  
  
7.  No **Editor do Gerenciador de Conexões de Arquivos Simples**, no tipo de caixa **Nome do Gerenciador de Conexões** digite **Dados do Erro**.  
  
8.  Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivo Simples** , clique em **Procurar**e localize a pasta em que o arquivo será armazenado.  
  
9. Na caixa de diálogo **Abrir** , para tipo de **Nome do arquivo**, digite **ErrorOutput.txt**e depois clique em **Abrir**.  
  
10. Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivo Simples** , verifique se a caixa **Localidade** contém Inglês (Estados Unidos) e **Página de código** contém 1252 (ANSI – Latim I).  
  
11. No painel de opções, clique em **Colunas**.  
  
    Observe que, além das colunas do arquivo de dados de origem, três colunas novas estão presentes: ErrorCode, ErrorColumn e ErrorDescription. Essas colunas são geradas pela saída de erro da transformação Pesquisa de Códigos de Moeda e pelo script na transformação Obter Descrição do Erro e podem ser usadas para diagnosticar a causa da linha com falha.  
  
12. Clique em **OK**.  
  
13. No **Editor de Destino de Arquivo Simples**, desmarque a caixa de seleção **Substituir dados no arquivo** .  
  
    Ao desmarcar essa caixa de seleção, os erros sobre as execuções de vários pacotes serão mantidos.  
  
14. No **Editor de Destino de Arquivo Simples**, clique em **Mapeamentos** para verificar se todas as colunas estão corretas. Como alternativa, você pode renomear as colunas no destino.  
  
15. Clique em **OK**.  
  
## <a name="next-steps"></a>Next Steps  
[Etapa 5: Testando o pacote de tutorial da Lição 4](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
  
  
