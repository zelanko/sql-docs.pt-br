---
title: Instalar pacotes de gerenciamento do SCOM - Analytics Platform System | Microsoft Docs
description: Siga estas etapas para baixar e instalar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para SQL Server PDW. Os pacotes de gerenciamento necessários para monitorar o SQL Server PDW do SCOM.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 163ab893074e171decb573d876c5f98334437985
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>Instalar pacotes de gerenciamento do SQL Server Operations Manager (SCOM) para o sistema de plataforma de análise
Siga estas etapas para baixar e instalar os pacotes de gerenciamento do System Center Operations Manager (SCOM) para SQL Server PDW. Os pacotes de gerenciamento necessários para monitorar o SQL Server PDW do SCOM.  
  
## <a name="BeforeBegin"></a>Antes de começar  
**Pré-requisitos**  
  
System Center Operations Manager deve estar instalado e em execução. PDW do SQL Server 2012 requer o System Center Operations Manager 2007 R2, System Center Operations Manager 2012 ou System Center Operations Manager 2012 service pack 1.  
  
## <a name="Step1"></a>Etapa 1: Baixar os pacotes de gerenciamento  
Para a carga de trabalho do PDW APS, baixe o [pacote de gerenciamento do System Center para Microsoft Analytics Platform System](http://go.microsoft.com/fwlink/?LinkId=396857).  
  
Para o gerenciamento de dispositivo, baixe o [o pacote de gerenciamento do SQL Server Appliance Base](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=11436).  
  
Para versões mais antigas do PDW sem APS, baixe o[System Center Monitoring Pack para Microsoft SQL Server 2012 Parallel aplicativo de Data Warehouse](http://go.microsoft.com/fwlink/p/?LinkId=282661).  
  
Para a carga de trabalho HDInsight, baixe o [pacote de gerenciamento do System Center para HDInsight](http://go.microsoft.com/fwlink/?LinkId=390208).  
  
## <a name="Step2"></a>Etapa 2: Instalar os pacotes de gerenciamento  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>Instalar o pacote de gerenciamento de Base de dispositivo do SQL Server  
  
1.  Para executar a instalação, clique duas vezes no baixado pacote de gerenciamento do SQL Server Appliance Base.  
  
2.  Aceite o contrato de licença e clique em **próximo**.  
  
    ![Aceite o contrato de licença](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  Selecione sua pasta de instalação, ou usar a pasta de instalação do pacote de gerenciamento padrão.  
  
    ![Selecione a pasta de instalação](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  Clique em **Instalar**.  
  
    ![Confirmar instalação](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  Clique em **Fechar**.  
  
    ![Clique em Fechar](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>Instalar o pacote de monitoramento para o dispositivo de PDW do SQL Server  
  
1.  Para executar a instalação, clique duas vezes no baixado pacote de gerenciamento do SQL Server PDW Appliance.  
  
2.  Aceite o contrato de licença e clique em **próximo**.  
  
    ![Aceite o contrato de licença](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  Escolha o diretório que conterá os arquivos extraídos. A pasta de instalação do pacote de gerenciamento padrão é mostrada por padrão. Selecione o padrão ou selecione sua pasta de instalação.  
  
    ![Selecionar pasta de instalação](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  Clique em **Instalar**.  
  
    ![Confirmar instalação](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  Clique em **Fechar**.  
  
    ![Instalação concluída do](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>Próxima etapa  
Agora que você tem os pacotes de gerenciamento instalados, prossiga para a próxima etapa: [importar o pacote de gerenciamento do SCOM para PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
