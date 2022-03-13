# proofing-

clear;
clc;
density_W = 8.33; %lb/gal
ProofingType = input('Enter 1 for final volume\nEnter 2 for inital spirit volume\nEnter 3 for initial water volume\n');
if ProofingType == 1
    disp('final volume detected')
    volumeF = input('Enter desired final volume in gallons:\n');
    proofF = input('Enter desired final proof:\n');
    proofI = input('Enter initial spirit proof:\n');
    massP_F = massPercent(proofF);
    massP_I = massPercent(proofI);
    density_F = density(proofF);
    density_I = density(proofI);
    massF = volumeF*density_F;
    massEtOH = massF*massP_F;
    massI = massEtOH/massP_I;
    volumeI = massI/density_I;
    massW = massF-massI;
    volumeW = massW/density_W;
    fprintf("Initial spirit volume of: %f0.2\n",volumeI);
    fprintf("Added water volume of: %f0.2\n",volumeW);
elseif ProofingType == 2
    disp('initial spirit volume dected')
    volumeS = input('Enter initial spirit volume in gallons:\n');
    proofI = input('Enter initial spirit proof:\n');
    proofF = input('Enter desired final proof:\n');
    massP_F = massPercent(proofF);
    massP_I = massPercent(proofI);
    density_F = density(proofF);
    density_I = density(proofI);
    massI = volumeS*density_I;
    mass_EtOH = massI*massP_I;
    massF = mass_EtOH/massP_F;
    volumeF = massF/density_F;
    massW = massF-massI;
    volumeW = massW/density_W;
    fprintf("Final spirit volume of: %f0.2\n",volumeF);
    fprintf("Added water volume of: %f0.2\n",volumeW);

elseif ProofingType == 3
    disp('initial water volume detected')
    volumeW = input('Enter initial water volume in gallons:\n');
    proofI = input('Enter initial spirit proof:\n');
    proofF = input('Enter desired final proof:\n');
    massP_F = massPercent(proofF);
    massP_I = massPercent(proofI);
    density_F = density(proofF);
    density_I = density(proofI);
    massW = volumeW*density_W;
    massI = massW*massP_F/(massP_I-massP_F);
    massEtOH = massI*massP_I;
    massF = massEtOH/massP_F;
    volumeF = massF/density_F;
    volumeI = massI/density_I;
    fprintf("Final spirit volume of: %f0.2\n",volumeF);
    fprintf("Initial spirit volume of: %f0.2\n",volumeI);
else
    disp('No value detected')
end


function massP = massPercent(proof)
if proof <= 30
    mass = 0.4022*proof;
elseif proof <= 70
    mass = 0.4272*proof-.7545;
elseif proof <= 100
    mass = .465*proof-3.3788;
elseif proof <= 130
    mass = .505*proof-7.3781;
elseif proof <= 160
    mass = 0.551*proof-13.375;
elseif proof <= 180
    mass = 0.5985*proof-20.944;
elseif proof < 200
    mass = .6531*proof-30.784;
else
    mass = 100;
end
massP = mass/100;
end


function density = density(proof)
EtOH_D = 6.59; %lb/gal
V_P = proof/200;
mass = V_P*EtOH_D;
massP = massPercent(proof);
density = mass/massP;
end
