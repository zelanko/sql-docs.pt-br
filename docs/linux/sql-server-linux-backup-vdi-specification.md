---
title: Especificação de backup de VDI – SQL Server em Linux
description: Especificação de backup da Interface de Dispositivo Virtual do SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.openlocfilehash: c2dafa8f1c0811771cbbc684b24d2c92e989dff5
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810970"
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>Especificação do SDK do cliente de VDI do SQL Server em Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento aborda as interfaces fornecidas pelo SDK do cliente de VDI (interface de dispositivo virtual) do SQL Server em Linux. Os ISVs (fornecedores independentes de software) podem usar a API (interface de programação de aplicativo) do Dispositivo de Backup Virtual para integrar o SQL Server a seus produtos. Em geral, o VDI no Linux se comporta da mesma forma que o VDI no Windows com as seguintes alterações:

- A memória compartilhada do Windows torna-se a memória compartilhada POSIX.
- Os semáforos do Windows se tornam semáforos POSIX.
- Os tipos do Windows, como HRESULT e DWORD, são alterados para equivalentes inteiros.
- As interfaces COM são removidas e substituídas por um par de classes C++.
- O SQL Server em Linux não dá suporte a instâncias nomeadas; portanto, as referências ao nome da instância foram removidas. 
- A biblioteca compartilhada é implementada no libsqlvdi.so instalado em /opt/mssql/lib/libsqlvdi.so

Este documento é um adendo ao **vbackup.chm** que fornece detalhes sobre a Especificação de VDI do MS SQL Server no Windows. Baixe a [Especificação de VDI do SQL no Windows](https://www.microsoft.com/download/details.aspx?id=17282).

Examine também a solução de backup de VDI de exemplo no [repositório GitHub de amostras do SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux).

## <a name="user-permissions-setup"></a>Configuração das permissões do usuário

No Linux, os primitivos POSIX são de propriedade do usuário que os cria e seu grupo padrão. Para os objetos criados pelo SQL Server, por padrão, eles serão propriedade do usuário mssql e do grupo mssql. Para permitir o compartilhamento entre o SQL Server e o cliente de VDI, um dos dois seguintes métodos é recomendado:

1. Executar o cliente de VDI como o usuário mssql
   
   Execute o seguinte comando para alternar para o usuário mssql:
   
   ```bash
   sudo su mssql
   ```

2. Adicione o usuário mssql ao grupo do vdiuser e o vdiuser ao grupo mssql.
   
   Execute os seguintes comandos:

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   Reinicie o servidor para selecionar novos grupos para o SQL Server e o vdiuser

## <a name="client-functions"></a>Funções de cliente

Este capítulo contém descrições de cada uma das funções de cliente. As descrições incluem as seguintes informações:

- Finalidade da função
- Sintaxe da função
- Lista de parâmetros
- Valores retornados
- Remarks

## <a name="clientvirtualdevicesetcreate"></a>ClientVirtualDeviceSet::Create

**Finalidade** Essa função cria o conjunto de dispositivos virtuais.

**Sintaxe**
   ```
   int ClientVirtualDeviceSet::Create (
   char *   name,       // name for the set
   VDConfig   * cfg     // configuration for the set
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| | **name** | Isso identifica o conjunto de dispositivos virtuais. As regras para nomes usados por CreateFileMapping() precisam ser seguidas. Qualquer caractere, exceto barra invertida (\) pode ser usado). Essa é uma cadeia de caracteres. É recomendável prefixar a cadeia de caracteres com o nome do produto ou da empresa do usuário e o nome do banco de dados. |
| |**cfg** | Essa é a configuração do conjunto de dispositivos virtuais. Para obter mais informações, confira "Configuração" mais adiante neste documento.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** | A função foi bem-sucedida. |
| |**VD_E_NOTSUPPORTED** |Um ou mais campos na configuração eram inválidos ou não tinham suporte. |
| |**VD_E_PROTOCOL** | O conjunto de dispositivos virtuais já existe.

**Comentários** O método Create deve ser chamado apenas uma vez por operação BACKUP ou RESTORE. Depois de invocar o método Close, o cliente pode reutilizar a interface para criar outro conjunto de dispositivos virtuais.

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**Finalidade** Essa função é usada para aguardar o servidor configurar o conjunto de dispositivos virtuais.
**Sintaxe**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| | **timeout** | Esse é o tempo limite em milissegundos. Use INFINITE ou qualquer inteiro negativo para impedir o tempo limite.
| | **cfg** | Após a execução bem-sucedida, isso conterá a configuração selecionada pelo servidor. Para obter mais informações, confira "Configuração" mais adiante neste documento.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** | A configuração foi retornada.
| |**VD_E_ABORT** |SignalAbort foi invocado.
| |**VD_E_TIMEOUT** |A função atingiu o tempo limite.

**Comentários** Essa função é bloqueada em um estado Passível de Alerta. Após a invocação bem-sucedida, os dispositivos do conjunto de dispositivos virtuais poderão ser abertos.


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**Finalidade** Essa função abre um dos dispositivos no conjunto de dispositivos virtuais.
**Sintaxe**
   ```
   int ClientVirtualDeviceSet::OpenDevice (
   char *           name,       // name for the set
   ClientVirtualDevice **       ppVirtualDevice // returns interface to device
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| | **name** |Isso identifica o conjunto de dispositivos virtuais.
| | **ppVirtualDevice** |Quando a função é bem-sucedida, um ponteiro para o dispositivo virtual é retornado. Esse dispositivo é usado para GetCommand e CompleteCommand.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_ABORT** | A anulação foi solicitada.
| |**VD_E_OPEN** |  Todos os dispositivos estão abertos.
| |**VD_E_PROTOCOL** |  O conjunto não está no estado de inicialização ou esse dispositivo específico já está aberto.
| |**VD_E_INVALID** |O nome do dispositivo é inválido. Não é um dos nomes considerados integrantes do conjunto.

**Comentários** VD_E_OPEN pode ser retornado sem problemas. O cliente pode chamar OpenDevice por meio de um loop até que esse código seja retornado.
Se mais de um dispositivo estiver configurado, por exemplo, *n* dispositivos, o conjunto de dispositivos virtuais retornará *n* interfaces de dispositivo exclusivas.

A função `GetConfiguration` pode ser usada para aguardar até que os dispositivos possam ser abertos.
Se essa função não for bem-sucedida, um valor nulo será retornado por meio do ppVirtualDevice.
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**Finalidade** Essa função é usada para obter o próximo comando na fila de um dispositivo. Quando solicitada, essa função aguarda o próximo comando.

**Sintaxe**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**timeout** |Esse é o tempo de espera, em milissegundos. Use INFINITE para aguardar indefinidamente. Use 0 para sondar um comando. VD_E_TIMEOUT será retornado se nenhum comando estiver disponível no momento. Se o tempo limite esgotar, o cliente decidirá a próxima ação.
| |**Tempo Limite** |Esse é o tempo de espera, em milissegundos. Use INFINITE ou um valor negativo para aguardar indefinidamente. Use 0 para sondar um comando. VD_E_TIMEOUT será retornado se nenhum comando estiver disponível antes que o tempo limite expire. Se o tempo limite esgotar, o cliente decidirá a próxima ação.
| |**ppCmd** |Quando um comando é retornado com êxito, o parâmetro retorna o endereço de um comando a ser executado. A memória retornada é somente leitura. Quando o comando é concluído, esse ponteiro é passado para a rotina CompleteCommand. Para obter detalhes sobre cada comando, confira "Comandos" mais adiante neste documento.
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |Foi efetuado fetch de um comando.
| |**VD_E_CLOSE** |O dispositivo foi fechado pelo servidor.
| |**VD_E_TIMEOUT** |Nenhum comando estava disponível e o tempo limite expirou.
| |**VD_E_ABORT** |O cliente ou o servidor usou o SignalAbort para forçar um desligamento.

**Comentários** Quando VD_E_CLOSE é retornado, o SQL Server fecha o dispositivo. Isso faz parte do desligamento normal. Depois que todos os dispositivos forem fechados, o cliente invocará ClientVirtualDeviceSet::Close para fechar o conjunto de dispositivos virtuais.
Quando essa rotina precisa ser bloqueada para aguardar um comando, o thread é deixado em uma condição Passível de Alerta.

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**Finalidade** Essa função é usada para notificar o SQL Server de que um comando foi concluído. As informações de conclusão apropriadas para o comando devem ser retornadas. Para obter mais informações, confira "Comandos" mais adiante neste documento.

**Sintaxe** 

   ```
   int ClientVirtualDevice::CompleteCommand (
   VDC_Command pCmd,        // the command
   int  completionCode,     // completion code
   unsigned long    bytesTransferred,   // bytes transferred
   int64_t  position        // current position
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**pCmd** |Esse é o endereço de um comando retornado anteriormente de ClientVirtualDevice::GetCommand.
| |**completionCode** |Esse é um código de status que indica o status da conclusão. Esse parâmetro precisa ser retornado para todos os comandos. O código retornado deve ser apropriado para o comando que está sendo executado. ERROR_SUCCESS é usado em todos os casos para indicar um comando executado com êxito. Para obter a lista completa de códigos possíveis, confira o arquivo vdierror.h. Uma lista de códigos de status típicos para cada comando será exibida em "Comandos" mais adiante neste documento.
| |**bytesTransferred** |Esse é o número de bytes transferidos com êxito. Isso é retornado somente para comandos de transferência de dados Leitura e Gravação.
| |**position** |Essa é uma resposta somente ao comando GetPosition.
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A conclusão foi anotada corretamente.
| |**VD_E_INVALID** |pCmd não era um comando ativo.
| |**VD_E_ABORT** |A anulação foi sinalizada.
| |**VD_E_PROTOCOL** |O dispositivo não está aberto.

**Comentários** Nenhum

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**Finalidade** Essa função é usada para sinalizar que um encerramento anormal deverá ocorrer.

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |None | Não aplicável
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR**|A notificação de anulação foi postada com êxito.

**Comentários** A qualquer momento, o cliente pode optar por anular a operação BACKUP ou RESTORE. Essa rotina sinaliza que todas as operações devem ser interrompidas. O estado do conjunto geral de dispositivos virtuais entra em um estado Encerrado de Forma Anormal. Nenhum outro comando é retornado nos dispositivos. Todos os comandos não concluídos são concluídos automaticamente, retornando ERROR_OPERATION_ABORTED como um código de conclusão. O cliente deverá chamar ClientVirtualDeviceSet::Close depois de encerrar com segurança qualquer uso pendente de buffers fornecidos ao cliente. Para obter mais informações, confira "Encerramento anormal" anteriormente neste documento.

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**Finalidade** Essa função fecha o conjunto de dispositivos virtuais criado por ClientVirtualDeviceSet::Create. Isso resulta na liberação de todos os recursos associados ao conjunto de dispositivos virtuais.

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |None |Não aplicável
        
| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |Isso é retornado quando o conjunto de dispositivos virtuais é fechado com êxito.
| |**VD_E_PROTOCOL** |Nenhuma ação foi executada porque o conjunto de dispositivos virtuais não estava aberto.
| |**VD_E_OPEN** |Os dispositivos ainda estavam abertos.

**Comentários** A invocação de Close é uma declaração de cliente que indica que todos os recursos usados pelo conjunto de dispositivos virtuais devem ser liberados. O cliente precisa garantir que todas as atividades que envolvem buffers de dados e dispositivos virtuais sejam encerradas antes da invocação de Close. Todas as interfaces de dispositivos virtuais retornadas por OpenDevice são invalidadas por Close.
O cliente tem permissão para emitir uma chamada Create na interface do conjunto de dispositivos virtuais depois que a chamada Close é retornada. Essa chamada criará um novo conjunto de dispositivos virtuais para uma operação BACKUP ou RESTORE seguinte.
Se Close for chamado quando um ou mais dispositivos virtuais ainda estiverem abertos, VD_E_OPEN será retornado. Nesse caso, SignalAbort é disparado internamente, para garantir um desligamento adequado, se possível. Os recursos de VDI são liberados. O cliente deve aguardar uma indicação de VD_E_CLOSE em cada dispositivo antes de invocar ClientVirtualDeviceSet::Close. Se o cliente souber que o conjunto de dispositivos virtuais já está em um estado Encerrado de Forma Anormal, ele não deverá esperar uma indicação VD_E_CLOSE de GetCommand e poderá invocar ClientVirtualDeviceSet::Close assim que a atividade nos buffers compartilhados for encerrada.
Para obter mais informações, confira "Encerramento anormal" anteriormente neste documento.

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**Finalidade** Essa função abre o conjunto de dispositivos virtuais em um cliente secundário. O cliente primário já precisa ter usado Create e GetConfiguration para configurar o conjunto de dispositivos virtuais.

**Sintaxe** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**setName** |Isso identifica o conjunto. Esse nome diferencia maiúsculas de minúsculas e precisa corresponder ao nome usado pelo cliente primário quando ele invoca ClientVirtualDeviceSet::Create.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_PROTOCOL** |O conjunto de dispositivos virtuais não foi criado, já foi aberto nesse cliente ou o conjunto de dispositivos virtuais não está pronto para aceitar solicitações abertas de clientes secundários.
| |**VD_E_ABORT** |A operação está sendo anulada.

**Comentários** Ao usar um modelo de processo múltiplo, o cliente primário é responsável por detectar o encerramento normal e anormal de clientes secundários.

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**Finalidade** Alguns aplicativos podem exigir mais de um processo para operar nos buffers retornados por ClientVirtualDevice::GetCommand. Nesses casos, o processo que recebe o comando pode usar GetBufferHandle para obter um identificador independente de processo que identifica o buffer. Esse identificador pode então ser comunicado a qualquer outro processo que também tenha o mesmo conjunto de dispositivos virtuais aberto. Esse processo usará ClientVirtualDeviceSet::MapBufferHandle para obter o endereço do buffer. O endereço provavelmente será um endereço diferente do que em seu parceiro, pois cada processo pode estar mapeando buffers em endereços diferentes.

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**pBuffer** |Esse é o endereço de um buffer obtido de um comando de Leitura ou Gravação.
| |**BufferHandle** |Um identificador exclusivo para o buffer é retornado.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_PROTOCOL** |O conjunto de dispositivos virtuais não está aberto no momento.
| |**VD_E_INVALID** |O pBuffer não é um endereço válido.

Comentários O processo que invoca a função GetBufferHandle é responsável por invocar ClientVirtualDevice::CompleteCommand quando a transferência de dados é concluída.

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**Finalidade** Essa função é usada para obter um endereço de buffer válido de um identificador de buffer obtido de algum outro processo. 

**Sintaxe** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| Parâmetros | Argumento | Explicação
| ----- | ----- | ------ |
| |**dwBuffer** |Esse é o identificador retornado por ClientVirtualDeviceSet::GetBufferHandle.
| |**ppBuffer** |Esse é o endereço do buffer que é válido no processo atual.

| Valores de retorno | Argumento | Explicação
| ----- | ----- | ------ |
| |**NOERROR** |A função foi bem-sucedida.
| |**VD_E_PROTOCOL** |O conjunto de dispositivos virtuais não está aberto no momento.
| |**VD_E_INVALID** |O ppBuffer é um identificador inválido.

**Comentários** Deve-se tomar cuidado para comunicar os identificadores corretamente. Os identificadores são locais para um único conjunto de dispositivos virtuais. Os processos de parceiros que compartilham um identificador precisam garantir que os identificadores de buffer sejam usados somente dentro do escopo do conjunto de dispositivos virtuais do qual o buffer foi originalmente obtido.


