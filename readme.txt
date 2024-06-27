Some sample code from Himax - 28/6/24
=========================================

These samples recived by email on 25/6/24. Should probably be added to the main SDK,
but parked here for the moment.

The email included this:

1    Sample code showing how to configure the HX6538 PA2/PA3 as an I2C slave, and exchange data.
Ans : You can refer to the attached sample code ~\scenario_app\i2c_slave_app\i2c_slave_app.c to configure PA2/PA3 as I2C slave and callback function.

void I2C_SLV_Init()
{
    uint32_t i2c_s_id = USE_DW_IIC_SLV_0;
    hx_drv_scu_set_PA2_pinmux(SCU_PA2_PINMUX_SB_I2C_S_SCL_0, 1);
    hx_drv_scu_set_PA3_pinmux(SCU_PA3_PINMUX_SB_I2C_S_SDA_0, 1);
    hx_drv_i2cs_init(i2c_s_id, HX_I2C_HOST_SLV_0_BASE);
    dev_iic_slv = hx_drv_i2cs_get_dev(i2c_s_id);
    dev_iic_slv->iic_control(DW_IIC_CMD_SET_TXCB, (void *)i2c_s_callback_fun_tx);
    dev_iic_slv->iic_control(DW_IIC_CMD_SET_RXCB, (void *)i2c_s_callback_fun_rx);
    dev_iic_slv->iic_control(DW_IIC_CMD_SET_ERRCB, (void *)i2c_s_callback_fun_err);
    dev_iic_slv->iic_control(DW_IIC_CMD_SLV_SET_SLV_ADDR, (void*)slave_addr);

    i2cs_read_enable(BUFF_SIZE);
}

2    Sample code showing how to place the HX6538 in a low power shutdown state and wake it with an interrupt.

Ans : You can refer to the attached sample code ~\scenario_app\seeed_sample\seeed_sample.c to configure HX6538 in a low power shutdown state and wake it with an interrupt(PA0(D0)/AON_GPIO0).

/**
* This function sets TIMER ID 2 or AON_GPIO0(PA0)/AON_GPIO1(PA1) as Power Down mode wake up sources.
* This function supports memory retention or memory no retention.
*
* @param timer_ms The wake up timer(millisecond).
* @param aon_gpio The index of the AON_GPIO pin to set as wake up source.
*                            0: AON_GPIO0(PA0), 1: AON_GPIO1(PA1), 0xFF: disable aon_gpio wake up.
* @param retention Memory retention or not.
*
*/
void app_pmu_enter_sleep(uint32_t timer_ms, uint32_t aon_gpio, uint32_t retention);
 
app_pmu_enter_sleep(0, 0, 0);         // AON_GPIO0(PA0) wake up, memory no retention

 



