---
title: 'Etapa 2: criar um arquivo corrompido | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f793f2cadf46d4a5431c01f5a1b1966ffad6fd55
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968196"
---
# <a name="step-2-creating-a-corrupted-file"></a>Etapa 2: Criar um arquivo corrompido
  Para demonstrar a configuração e o tratamento de erros de transformação, você terá que criar um arquivo simples de amostra que no processamento causa a falha de um componente.  
  
 Nesta tarefa, você criará uma cópia de um arquivo simples de amostra existente. Você deverá então abrir o arquivo no Bloco de Notas e editar a coluna **CurrencyID** para certificar-se de que não produzirá uma correspondência durante a pesquisa de transformações. Quando o arquivo novo for processado, a falha na pesquisa irá causar a falha da transformação Pesquisa de Códigos de Moeda e criará, portanto, uma falha no resto do pacote. Depois de criar o arquivo de amostra corrompido, você executará o pacote para exibir a falha do pacote.  
  
### <a name="to-create-a-corrupted-sample-flat-file"></a>Para criar um arquivo simples de amostra corrompido  
  
1.  No Bloco de Notas ou em qualquer outro editor de texto, abra o arquivo Currency_VEB.txt.  
  
     Os dados de exemplo estão incluídos nos pacotes de lição do SSIS. Para baixar os dados de exemplo e os pacotes de lição, faça o seguinte.  
  
    1.  Navegue até [Integration Services exemplos de produto](https://go.microsoft.com/fwlink/?LinkID=267527).  
  
    2.  Clique na guia **downloads** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
2.  Use o recurso Localizar e substituir do editor de texto para localizar todas as instâncias do `VEB` e substituí-las por `BAD` .  
  
3.  Na mesma pasta que os outros arquivos de dados de exemplo, salve o arquivo modificado como `Currency_BAD.txt` .  
  
    > [!IMPORTANT]  
    >  Verifique se o `Currency_BAD.txt` está salvo na mesma pasta que os outros arquivos de dados de exemplo.  
  
4.  Feche seu editor de texto.  
  
### <a name="to-verify-that-an-error-will-occur-during-run-time"></a>Para verificar se um erro acontecerá durante o tempo de execução  
  
1.  No menu **depurar** , clique em **Iniciar Depuração**.  
  
     Na terceira repetição do fluxo de dados, uma transformação Pesquisa de Códigos de Moeda tenta processar o arquivo Currency_BAD.txt e a transformação irá falhar. O fracasso da transformação fará o pacote inteiro falhar.  
  
2.  No menu **Depurar** , clique em **Parar Depuração**.  
  
3.  Na superfície de design, clique na guia **Resultados da Execução** .  
  
4.  Procure no log e verifique se o seguinte erro sem-tratamento ocorreu:  
  
     `[Lookup Currency Key[27]] Error: Row yielded no match during lookup.`  
  
    > [!NOTE]  
    >  O número 27 é a ID do componente. Esse valor é atribuído quando você cria o fluxo de dados, ou seja, o valor do seu pacote pode ser diferente.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Etapa 3: Adicionar redirecionamento de fluxo de erro](lesson-4-3-adding-error-flow-redirection.md)  
  
  
