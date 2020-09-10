.. code-block:: MATLAB
    %Q-1
    c = physconst('lightspeed');
    d=10e3 %distance in Km
    freq = (50:1000).'*1e9; %frequency range GHz
    pathloss = fspl(d,c./freq);

    figure(1); %plot
    loglog(freq/1e9,pathloss);
    grid on;
    ylabel('Path Loss(dB)')
    xlabel('Frequency (GHz)')
    title('Free Space Path Loss');

    %Q-2
    %Rain Attenuation
    rainrate=20;  % rain rate in mm/h 
    el = 0;     % 0 degree elevation 
    tau = 0;    % horizontal polarization 
    for m = 1:numel(freq)
        rainloss(:,m) = rainpl(d,freq(m),rainrate,el,tau)';
    end
    figure(2); %plot
    loglog(freq/1e9,rainloss); 
    grid on;
    xlabel('Frequency (GHz)'); 
    ylabel('Rain Attenuation (dB/km)') 
    title('Rain Attenuation'); 

    %Fog Attenuation
    T = 31;                  % Ambient Temperature
    waterdensity = 0.5;      %water density in g/m^3 
    for m = 1: numel(freq)
        fogloss(:,m) = fogpl(d,freq(m),T,waterdensity)'; 
    end 
    figure(3);%plot
    loglog(freq/1e9,fogloss); 
    grid on; 
    xlabel('Frequency (GHz)'); 
    ylabel('Fog Attenuation (dB/km)') 
    title('Fog Attenuation'); 

    %Atmospheric Gas Attenuation
    P = 101300; % dry air pressure in Pa 
    ROU = 7.5;  % water vapour density in g/m^3 
    for m = 1: numel(freq)
        gasloss(:,m)= gaspl(d,freq(m),T,P,ROU);
    end
    figure(4);%plot
    loglog(freq/1e9,gasloss); 
    grid on; 
    xlabel('Frequency (GHz)'); 
    ylabel('Atmospheric Gas Attenuation (dB/km)') 
    title('Atmospheric Gas Attenuation'); 

    %Q-3
    %Path Loss for 10km Distance
    figure(5)
    semilogy(freq/1e9,pathloss+rainloss+fogloss+gasloss); %plot total path loss with frequency
    grid on; 
    xlabel('Propagation Frequance (GHz)'); 
    ylabel('Path Loss (dB)');
    title('Path Loss for 10km Distance'); 

    %Q-4
    fc = 50e9;
    R = (0:10000).';
    apathloss = fspl(R,c/fc);
    rr = 20;
    el = 0;     % 0 degree elevation 
    tau = 0;    % horizontal polarization 
    arainloss = rainpl(R,fc,rr,el,tau);
    M = 0.5;  
    afogloss = fogpl(R,fc,T,M);
    agasloss = gaspl(R,fc,T,P,ROU); 
    P=103.98  %power release by transmitter antenna
    figure(6)
    plot(R/1000,P-(apathloss+arainloss+afogloss+agasloss));
    grid on; 
    xlabel('Propagation Distance (km)'); 
    ylabel('Power(dB)');
    title('Power variation for 50 GHz Signal'); 

