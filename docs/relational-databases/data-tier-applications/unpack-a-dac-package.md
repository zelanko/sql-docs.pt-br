---
title: Desempacotar um pacote de DAC | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- wizard [DAC], unpack
- data-tier application [SQL Server], unpack
- How to [DAC], unpack
- unpack DAC
ms.assetid: 697b69b3-f157-4e22-ac4e-f65c5fc2d0ad
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dc4498e01b9f72d8ef2cd9f13b137c67f48d63ff
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="unpack-a-dac-package"></a>Desempacotar um pacote de DAC
  Use a caixa de diálogo Desempacotar Aplicativo da Camada de Dados para descompactar os scripts e arquivos de um pacote de DAC (aplicativo da camada de dados). Os scripts e arquivos são colocados em uma pasta onde podem ser examinados antes do pacote ser usado para implantar o DAC em um sistema de produção. O conteúdo de um DAC também pode ser comparado com o conteúdo de outro pacote desempacotado em outra pasta.  
  
1.  **Antes de começar:**  [Segurança](#Security)  
  
2.  **Para desempacotar um DAC, usando:**  [Caixa de diálogo Desempacotar Aplicativo da Camada de Dados](#UnpackDACDial), [Examinar o Conteúdo de um Pacote de DAC](#ExamDACPack)  
  
##  <a name="Security"></a> Segurança  
 Recomendamos não implantar um pacote de DAC de origens desconhecidas ou não confiáveis. Como os DACs podem conter código mal-intencionado que pode executar código [!INCLUDE[tsql](../../includes/tsql-md.md)] sem finalidade ou provocar erros modificando o esquema. Antes de usar um DAC de uma origem desconhecida ou não confiável, implante-o em uma instância de teste isolada do [!INCLUDE[ssDE](../../includes/ssde-md.md)], desempacote o DAC e examine o código, como procedimentos armazenados ou outro código definido pelo usuário.  
  
##  <a name="UnpackDACDial"></a> Caixa de diálogo Desempacotar Aplicativo da Camada de Dados  
 **Para desempacotar um arquivo do pacote de DAC**  
  
-   No **Windows Explorer**, navegue até a localização de um arquivo de pacote de DAC (.dacpac).  
  
-   Use um destes dois métodos para abrir a caixa de diálogo Desempacotar Aplicativo da Camada de Dados:  
  
    1.  Clique com o botão direito do mouse no arquivo de pacote de DAC (.dacpac) e selecione **Desempacotar**.  
  
    2.  Clique duas vezes no arquivo do pacote de DAC.  
  
-   Conclua os diálogos:  
  
    -   [Desempacotar Arquivo de Pacote de DAC do Microsoft SQL Server](#Unpack)  
  
    -   [Procurar Pasta](#Browse)  
  
###  <a name="Unpack"></a> Desempacotar Arquivo de Pacote de DAC do Microsoft SQL Server  
 Use esta página para especificar a pasta de destino na qual colocar os arquivos desempacotados e execute a operação e desempacotamento.  
  
 **Os arquivos serão desempacotados nesta pasta:** – Especifique o caminho completo da pasta para os arquivos desempacotados. Se a pasta existir e você conhecer o caminho completo, digite o caminho na caixa. Caso contrário, clique no botão **Procurar** para navegar para uma pasta ou criar uma nova pasta.  
  
 **Procurar** – Abre a página **Procurar Pasta** , em que é possível escolher uma pasta navegando pela hierarquia de arquivos ou criar uma nova pasta.  
  
 **Desempacotar** – Inicia a operação de desempacotamento.  
  
 **Cancelar** – Encerra a caixa de diálogo sem desempacotar o pacote de DAC.  
  
###  <a name="Browse"></a> Procurar Pasta  
 Use esta página para escolher a pasta de destino para a operação de desempacotamento. Como opção, você também pode criar uma nova pasta.  
  
 **Lista de pastas** – Exibe a hierarquia de arquivos de seu computador. Expanda os nós para navegar para a pasta na qual desempacotar o pacote de DAC. Clique na pasta e, em seguida, clique em **OK**.  
  
 **Criar Nova Pasta** – Abre uma caixa de diálogo na qual é possível especificar o nome de uma nova pasta a ser criada na pasta selecionada atualmente na hierarquia de pastas.  
  
 **OK** – Coloca o caminho para a pasta selecionada na caixa **Os arquivos serão desempacotados nesta pasta** da página **Desempacotar Arquivo de Pacote de DAC** e retorna para a página.  
  
 **Cancelar** – Encerra a caixa de diálogo sem selecionar uma pasta.  
  
##  <a name="ExamDACPack"></a> Examinar o Conteúdo de um Pacote de DAC  
 Depois de desempacotar o pacote, você poderá examinar os arquivos gerados pela caixa de diálogo **Desempacotar Aplicativo da Camada de Dados** . A caixa de diálogo cria os arquivos a seguir na pasta de destino selecionada:  
  
1.  Um script do Transact-SQL que contém as instruções para criar os objetos definidos no DAC. O nome do arquivo é *DACName*.sql, em que *DACName* é o nome do DAC.  
  
2.  Todos os arquivos XML do pacote.  
  
3.  Todos os arquivos da seção Arquivos Extras do DAC, como os arquivos de pré-implantação ou de pós-implantação do DAC.  
  
 Para obter mais informações, consulte [Validate a DAC Package](../../relational-databases/data-tier-applications/validate-a-dac-package.md).  
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos da camada de dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Implantar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Atualizar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)  
  
  
