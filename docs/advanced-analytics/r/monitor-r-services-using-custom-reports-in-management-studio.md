---
title: "Monitorar R Services usando relatórios personalizados no Management Studio | Microsoft Docs"
ms.custom: 
ms.date: 02/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5933c72c-ba63-4966-b882-75719ef8428e
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 14f6d6d7373afd452f06acae43f7023de136bc71
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="monitor-r-services-using-custom-reports-in-management-studio"></a>Monitorar serviços R usando relatórios personalizados no Management Studio
Para tornar mais fácil de gerenciar os serviços do SQL Server R, a equipe de produto forneceu um número de exemplos de relatórios personalizados que você pode adicionar ao SQL Server Management Studio, para exibir detalhes de serviços R, como:

- Uma lista de sessões R ativas
- A configuração R da instância atual
- Estatísticas de execução de para tempo de execução R
- Lista de eventos estendidos para serviços R
- Uma lista de pacotes R instalados na instância atual

Este tópico explica como instalar e usar os relatórios. Para obter mais informações sobre relatórios personalizados no Management Studio, consulte [relatórios personalizados no Management Studio](~/ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>Como instalar os relatórios

Os relatórios são criados usando o SQL Server Reporting Services, mas podem ser usados diretamente no SQL Server Management Studio, mesmo se o Reporting Services não está instalado em sua instância. 

Para usar esses relatórios:

* Baixe os arquivos RDL do repositório GitHub para exemplos de produto do SQL Server.
* Adicione os arquivos na pasta de relatórios personalizados usada pelo SQL Server Management Studio.
* Abra os relatórios no SQL Server Management Studio.


### <a name="step-1-download-the-reports"></a>Etapa 1. Baixe os relatórios

1. Abra o repositório GitHub que contém [Amostras de produto do SQL Server](https://github.com/Microsoft/sql-server-samples) e baixe os relatórios de exemplo desta página: 

   + [Relatórios personalizados SSMS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/ssms-custom-reports)
      
2. Para baixar os exemplos, você também pode fazer logon no GitHub e fazer uma bifurcação local dos exemplos. 

### <a name="step-2-copy-the-reports-to-management-studio"></a>Etapa 2. Copie os relatórios para o Management Studio

3. Localize a pasta de relatórios personalizados usada pelo SQL Server Management Studio. Por padrão, os relatórios personalizados são armazenados nessa pasta:
    
   `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

   No entanto, você pode especificar uma pasta diferente ou criar subpastas.

4. Copie os arquivos *. RDL para a pasta de relatórios personalizados.


### <a name="step-3-run-the-reports"></a>Etapa 3. Execute os relatórios

5. No Management Studio, clique com botão direito do mouse do nó **Databases** para a instância em que você deseja executar os relatórios.
6. Clique em **relatórios**e, em seguida, clique em **relatórios personalizados**. 
7. Na caixa de diálogo **Abrir arquivo** , localize a pasta de relatórios personalizados.
8. Selecione um dos arquivos RDL baixados e, em seguida, clique em **Abrir**.

> [!IMPORTANT]
> Em alguns computadores, como aqueles com dispositivos com alto DPI ou maior que a resolução de 1080p de exibição ou em algumas sessões da área de trabalho remota, esses relatórios não podem ser usados. Há um bug no controle do Visualizador de Relatórios no SSMS que trava o relatório.  


## <a name="report-list"></a>Lista de relatórios

O repositório de exemplos de produto no GitHub atualmente inclui os seguintes relatórios de serviços do SQL Server R:

+ **Serviços R – sessões ativas**

  Use esse relatório para exibir os usuários atualmente conectados à instância do SQL e executar trabalhos R. 
  
+ **Serviços R – configuração**

  Use este relatório para exibir as propriedades do tempo de execução R e a configuração dos serviços R. O relatório indica se uma reinicialização é necessária e verificará se há protocolos de rede necessários. 
  
  Autenticação implícita é necessária para executar o R em um contexto de computação do SQL, para verificar isso, o relatório verifica se existe um logon de banco de dados para o grupo SQLRUserGroup.

  > [!NOTE]
  > Para obter mais informações sobre esses campos, consulte [metadados de pacote](http://r-pkgs.had.co.nz/description.html), por Hadley Wickam. Por exemplo, o campo *Nickname* para o tempo de execução R foi introduzido para ajudar a diferenciar entre as versões. 

 + **Serviços R – configurar instância** 

   Este relatório destina-se a ajudá-lo a configurar os serviços R após a instalação. Você pode executá-lo do relatório anterior se os Serviços R não estão configurados corretamente.
 
+ **Serviços R – Estatísticas de execução**

  Use esse relatório para exibir as estatísticas de execução dos serviços R. Por exemplo, você pode obter o número total de scripts R que foram executados, o número de execuções paralelas e as funções de RevoScaleR usadas com mais frequência.
  Atualmente o relatório monitora somente as estatísticas para funções do pacote RevoScaleR.
  Clique em **Exibir SQL Script** para obter o código T-SQL para este relatório. 

+ **Serviços R – eventos estendidos**

  Use esse relatório para exibir uma lista dos eventos estendidos que estão disponíveis para monitorar a execução do script R. 
  Clique em **Exibir SQL Script** para obter o código T-SQL para este relatório.

+ **Serviços R – pacotes**

  Use esse relatório para exibir uma lista dos pacotes R instalados na instância do SQL Server. Atualmente, o relatório inclui essas propriedades de pacote: 
  + Pacote (nome)
  + Versão 
  + Depende
  + Licença
  + Versão
  + Caminho de biblioteca

+ **Serviços R – utilização de recursos**

  Use esse relatório para exibir o consumo de recursos de CPU, memória e E/S por execução de scripts R do SQL Server. Você também pode exibir a configuração de memória de pools de recursos externos. 


## <a name="see-also"></a>Consulte também

[Monitorar os serviços R](../../advanced-analytics/r-services/monitoring-r-services.md)

[Eventos estendidos para serviços R](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)


