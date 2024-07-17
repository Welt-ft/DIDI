// xml 

<dependencies>
    <dependency>
        <groupId>com.pi4j</groupId>
        <artifactId>pi4j-core</artifactId>
        <version>1.2</version>
    </dependency>
</dependencies>

// java 

import com.pi4j.io.gpio.GpioController;
import com.pi4j.io.gpio.GpioFactory;
import com.pi4j.io.gpio.GpioPinPwmOutput;
import com.pi4j.io.gpio.Pin;
import com.pi4j.io.gpio.PinState;
import com.pi4j.io.gpio.RaspiPin;

public class RGBLedControl {

    private static GpioController gpio;
    private static GpioPinPwmOutput redPin;
    private static GpioPinPwmOutput greenPin;
    private static GpioPinPwmOutput bluePin;

    public static void main(String[] args) {
        gpio = GpioFactory.getInstance();

        // Defina os pinos GPIO para os pinos PWM do LED RGB
        redPin = gpio.provisionPwmOutputPin(RaspiPin.GPIO_01);
        greenPin = gpio.provisionPwmOutputPin(RaspiPin.GPIO_02);
        bluePin = gpio.provisionPwmOutputPin(RaspiPin.GPIO_03);

        redPin.setPwmRange(100);
        greenPin.setPwmRange(100);
        bluePin.setPwmRange(100);

        // Configuração inicial (LED apagado)
        setColor(0, 0, 0);

        // Altere as cores para testar
        setColor(100, 0, 0); // vermelho
        delay(1000);

        setColor(0, 100, 0); // verde
        delay(1000);

        setColor(0, 0, 100); // azul
        delay(1000);

        setColor(100, 100, 0); // amarelo
        delay(1000);

        setColor(0, 100, 100); // ciano
        delay(1000);

        setColor(100, 0, 100); // magenta
        delay(1000);

        setColor(100, 100, 100); // branco
        delay(1000);

        // Desligue o LED
        setColor(0, 0, 0);

        gpio.shutdown();
    }

    private static void setColor(int red, int green, int blue) {
        redPin.setPwm(red);
        greenPin.setPwm(green);
        bluePin.setPwm(blue);
    }

    private static void delay(int ms) {
        try {
            Thread.sleep(ms);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}
