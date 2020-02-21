---
title: Adicionar um instantâneo ao histórico de relatórios – Reporting Services | Microsoft Docs
ms.prod: reporting-services
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 06/26/2019
ms.openlocfilehash: 2ada64f14c3564bd1e6c9846f890fdd8b287cb6f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68251937"
---
# <a name="add-a-snapshot-to-report-history"></a>Adicionar um instantâneo ao histórico de relatório

O histórico de relatórios é uma coleção de instantâneos de relatórios que você cria. Um instantâneo de relatório é um relatório que contém informações sobre layout e resultados de consulta que foram recuperados em um momento determinado. Diferente dos relatórios sob demanda, que obtêm resultados de consulta atualizados quando o relatório é selecionado, os instantâneos de relatório são processados em uma agenda e salvos em um servidor de relatório. Quando você seleciona um instantâneo de relatório para exibição, o servidor de relatório recupera o relatório armazenado do banco de dados do servidor e mostra os dados e o layout correspondentes ao momento em que o instantâneo foi criado.  
  
Os instantâneos de relatório não são salvos em um formato de renderização específico. Em vez disso, os instantâneos de relatório são renderizados em um formato de exibição final (como HTML) somente quando solicitado por um usuário ou aplicativo. A renderização adiada deixa o instantâneo portátil. O relatório pode ser renderizado no formato correto para a solicitação do dispositivo ou navegador da Web.  
  
## <a name="to-manually-add-snapshots-to-report-history"></a>Para adicionar manualmente instantâneos ao histórico de relatórios
  
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

1. No Gerenciador de Relatórios, navegue até a página **Conteúdo** , focalize o item cujo histórico você quer exibir e clique na seta suspensa.
  
2. No menu suspenso, clique em **Exibir Histórico de Relatório**.  
  
3. Clique em **Novo Instantâneo**. Um novo instantâneo é criado na coluna **Quando Executado** .  
    > [!NOTE]
    > Para habilitar a criação de instantâneos, o administrador deve configurar o histórico de relatórios para **Permitir que o histórico seja criado manualmente**. Para obter mais informações, consulte [Limitar o histórico de relatório &#40;Gerenciador de Relatórios&#41;](../reports/limit-report-history-report-manager.md).

4. Clique em **Aplicar**.
  
## <a name="to-automatically-add-all-snapshots-to-report-history"></a>Para adicionar automaticamente todos os instantâneos ao histórico de relatórios  
  
1. Para um relatório que já foi configurado para ser executado como um instantâneo de execução de relatório, é possível definir propriedades adicionais para salvar uma cópia do instantâneo no histórico de relatórios sempre que o instantâneo for atualizado.  
  
2. No Gerenciador de Relatórios, navegue até a página **Conteúdo** , focalize o item cujo histórico você quer exibir e clique na seta suspensa.  
  
3. No menu suspenso, clique em **Gerenciar**.  
  
4. Clique em **Opções de Instantâneo**.  
  
5. Marque a caixa de seleção **Armazenar todos os instantâneos de execução de relatórios no histórico**.  
  
6. Clique em **Aplicar**.  
  
## <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>Para adicionar automaticamente instantâneos ao histórico de relatórios com base em um agendamento  
  
1. No Gerenciador de Relatórios, navegue até a página **Conteúdo** , focalize o item cujo histórico você quer exibir e clique na seta suspensa.  
  
2. No menu suspenso, clique em **Gerenciar**.  
  
3. Clique em **Opções de Instantâneo**.  
  
4. Marque a caixa de seleção para **Usar o agendamento a seguir para adicionar instantâneos ao histórico de relatório**. Execute uma das ações a seguir:  
  
    - Selecione **Agendamento específico do relatório**. Preencha os detalhes do agendamento, selecione as datas de início e término e clique em **OK**.  

    - Selecione **Agendamento compartilhado**. Na lista, selecione a agenda desejada.  

5. Clique em **Aplicar**.  
  
## <a name="see-also"></a>Confira também

- [Configurar propriedades de execução de um relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)
- [Limitar o histórico de relatórios &#40;Gerenciador de Relatórios&#41;](../../reporting-services/reports/limit-report-history-report-manager.md)
- [Agendas](../../reporting-services/subscriptions/schedules.md)   
- [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="to-manually-add-snapshots-to-report-history"></a>Para adicionar manualmente instantâneos ao histórico de relatórios
  
1. No porta da Web, navegue até o item cujo histórico deseja ver e clique com o botão direito do mouse sobre ele.  
  
2. No menu suspenso, selecione **Gerenciar**.  
  
3. Selecione a guia **Instantâneos do histórico**.  
  
4. Na página **Instantâneos do histórico**, selecione **Novo instantâneo do histórico**. Um instantâneo será criado e aparecerá abaixo com a data e a hora atuais na coluna **Criado em**.  
  
    > [!NOTE]
    > Para habilitar a criação de instantâneos, o administrador deve configurar o histórico de relatórios para **Permitir que o histórico seja criado manualmente**. Para obter mais informações, confira [Limitar o histórico de relatórios (portal da Web)](../../reporting-services/reports/limit-report-history-report-manager.md).

## <a name="to-add-snapshots-via-a-schedule-to-report-history"></a>Para adicionar instantâneos ao histórico de relatórios por meio de um agendamento

1. No porta da Web, navegue até o item cujo histórico deseja ver e clique com o botão direito do mouse sobre ele.  
  
2. No menu suspenso, selecione **Gerenciar**.  
  
3. Selecione a guia **Instantâneos do histórico**.  
  
4. Na página **Instantâneos do histórico**, selecione o botão **Agendamento e configurações**.  
  
5. Na seção **Agendamento**, selecione uma ou ambas as opções abaixo se pelo menos uma delas ainda não houver sido selecionada:
    - **Criar instantâneos de histórico segundo uma agenda**.  
    - **Permitir que as pessoas criem instantâneos manualmente**.  
  
6. Na seção **Avançado**, selecione **Reter todos os instantâneos do histórico**.  
  
7. Opcionalmente, marque a caixa de seleção para **Salvar também os instantâneos do cache no histórico de relatórios**.  
  
8.  Selecione **Aplicar** para salvar as configurações.  

    > [!NOTE]  
    > Para habilitar a criação de instantâneos, o administrador deve configurar o histórico de relatórios para **Permitir que o histórico seja criado manualmente**. Para obter mais informações, confira [Limitar o histórico de relatórios (portal da Web)](../../reporting-services/reports/limit-report-history-report-manager.md).

9.  Clique em **Aplicar**.

## <a name="to-automatically-add-all-snapshots-to-report-history"></a>Para adicionar automaticamente todos os instantâneos ao histórico de relatórios  
  
1. Para um relatório que já foi configurado para ser executado como um instantâneo de execução de relatório, é possível definir propriedades adicionais para salvar uma cópia do instantâneo no histórico de relatórios sempre que o instantâneo for atualizado.  
  
2. No porta da Web, navegue até o item cujo histórico deseja ver e clique com o botão direito do mouse sobre ele.  
  
3. No menu suspenso, selecione **Gerenciar**.  
  
4. Selecione a guia **Instantâneos do histórico**.  
  
5. Na página **Instantâneos do histórico**, selecione o botão **Agendamento e configurações**.  
  
6. Na seção **Agendamento**, selecione uma ou ambas as opções abaixo se pelo menos uma delas ainda não houver sido selecionada:
    - **Criar instantâneos de histórico segundo uma agenda**.  
    - **Permitir que as pessoas criem instantâneos manualmente**.  
  
7. Na seção **Avançado**, selecione **Reter todos os instantâneos do histórico**.  
  
8. Opcionalmente, marque a caixa de seleção para **Salvar também os instantâneos do cache no histórico de relatórios**.  
  
9. Selecione **Aplicar** para salvar as configurações.  
  
## <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>Para adicionar automaticamente instantâneos ao histórico de relatórios com base em um agendamento  
  
1. No porta da Web, navegue até o item cujo histórico deseja ver e clique com o botão direito do mouse sobre ele.  
  
2. No menu suspenso, selecione **Gerenciar**.  
  
3. Selecione a guia **Instantâneos do histórico**.  
  
4. Na página **Instantâneos do histórico**, selecione o botão **Agendamento e configurações**.  
  
5. Marque a caixa de seleção para **Usar o agendamento a seguir para adicionar instantâneos ao histórico de relatório**. Execute uma das ações a seguir:  
  
    - Selecione **Agendamento específico do relatório**. Preencha os detalhes do agendamento, selecione as datas de início e término e clique em **OK**.  

    - Selecione **Agendamento compartilhado**. Na lista, selecione a agenda desejada.  

5. Clique em **Aplicar**.  
  
## <a name="see-also"></a>Confira também

- [Configurar propriedades de execução de um relatório (portal da Web)](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)
- [Limitar o histórico de relatório (portal da Web)](../../reporting-services/reports/limit-report-history-report-manager.md)
- [Agendas](../../reporting-services/subscriptions/schedules.md)   
- [o portal da Web &#40;Modo nativo do SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)

::: moniker-end