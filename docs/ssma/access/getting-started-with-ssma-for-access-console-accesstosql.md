---
title: Guia de Introdução ao SSMA para Access Console (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
caps.latest.revision: 21
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c37a486c560a5dc0cb6298f93b4486accc18354b
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773912"
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>Guia de Introdução ao SSMA para Access Console (AccessToSQL)
Esta seção descreve o procedimento para iniciar e começar a trabalhar com o aplicativo de console de acesso. Também é listado, aqui, são as convenções usadas em uma janela de saída do Console SSMA típica.  
  
## <a name="launching-ssma-console"></a>Iniciar Console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console SSMA:  
  
1.  Vá para **iniciar** e aponte para **todos os programas**.  
  
2.  Clique o **SQL Server Migration Assistant para o Prompt de comando de acesso** atalho.  
  
    Exibe o menu de uso do Console SSMA e `(/? Help)`, para ajudá-lo a começar com o aplicativo de console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimento para usar o Console do SSMA  
Depois que o console é iniciado com êxito em seu sistema Windows, você pode usar as etapas a seguir para trabalhar nela:  
  
1.  Configure o Console do SSMA através dos arquivos de script. Para obter mais informações sobre esta seção, consulte [criando arquivos de Script &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md).  
  
2.  [Criando arquivos do valor da variável &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [Criar os arquivos de Conexão de servidor &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  [Executar o Console SSMA &#40;AccessToSQL&#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md) com base em suas necessidades de projeto  
  
Recursos adicionais:  
  
1.  [Especifique uma senha](http://msdn.microsoft.com/en-us/b099d0f9-dd37-4c87-8b6f-ed0177881ea4) e exportar / importá-lo em outros computadores da janela  
  
2.  [Gerar relatórios](http://msdn.microsoft.com/en-us/abb4264a-622e-4215-af5b-14e309b8a399) para exibir o xml detalhado a saída de relatórios para avaliação /conversion e migração de dados. Relatórios de erro detalhadas também podem ser gerados para os comandos de atualização e sincronização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída do Console SSMA  
Depois de executar os comandos de script do SSMA e opções, o programa do console exibe os resultados e mensagens (informações de erro, etc.) para o usuário no console ou se necessário, redireciona para um arquivo de saída xml. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto em branco indica comandos de script de arquivo; a cor verde representa um prompt de entrada do usuário e assim por diante.  
  
![Saída do Console SSMA](../../ssma/access/media/ssmaconsoleoutput.jpg "saída do Console SSMA")  
  
Interpretação de cor da saída do console na tabela a seguir:  
  
|Color|Description|  
|---------|---------------|  
|Vermelho|Erro fatal durante a execução|  
|Cinza|Carimbo de data e hora, a mensagem para o usuário|  
|Branco|Comandos do arquivo de script, o tipo de mensagem|  
|Amarelo|Aviso|  
|Verde|Solicitar entrada do usuário|  
|Ciano|Início, término e o resultado de uma operação|  
  
## <a name="see-also"></a>Consulte também  
[Instalando o Assistente de migração do SQL Server para Access](http://msdn.microsoft.com/en-us/dd50eebd-75df-4e0d-8c4d-88b511aae4c7)  
  
