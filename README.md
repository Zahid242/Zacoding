# Zacoding
%%General constellation for Regular Hexagonal QAM%%

function []= hexconst(M) %M=16,64,256,... 
d=1; %side length
L=sqrt(M);
rows=L; cols=L;
X_centers=repmat((-(L-.5):2:(L-1.5)),rows,1);
Y_centers = repmat(((L-1)*sqrt(3)/2:-sqrt(3):-(L-1)*sqrt(3)/2)',1,cols);

odd_offset=d;
X_centers(1:2:end,:)=X_centers(1:2:end,:)+odd_offset;

X_vertices = zeros(rows,cols,6); 
Y_vertices = zeros(rows,cols,6);

% topleft
X_vertices(:,:,1) = X_centers-d;
Y_vertices(:,:,1) = Y_centers+d/2;
% top
X_vertices(:,:,2) = X_centers;
Y_vertices(:,:,2) = Y_centers+d+.25;
% topright
X_vertices(:,:,3) = X_centers+d;
Y_vertices(:,:,3) = Y_centers+d/2;
% botright
X_vertices(:,:,4) = X_centers+d;
Y_vertices(:,:,4) = Y_centers-d/2;
% bot
X_vertices(:,:,5) = X_centers;
Y_vertices(:,:,5) = Y_centers-d-.25;
% botleft
X_vertices(:,:,6) = X_centers-d;
Y_vertices(:,:,6) = Y_centers-d/2;

X_vertices=permute(X_vertices,[3 1 2]);
X_vertices=reshape(X_vertices,6,[]);

Y_vertices=permute(Y_vertices,[3 1 2]);
Y_vertices=reshape(Y_vertices,6,[]);
%Plots
hexagons = fill(X_vertices,Y_vertices,ones(1,M));
hold on;
set(hexagons,'facealpha',0); %change to get color (0=white)
plot(X_centers,Y_centers,'ro','linewidth',6);
%set(gca,'xtick',[],'ytick',[]);
xlim([-(L+2) (L+2)]);
ylim([-(L+2) (L+2)]);
line(xlim,[0 0],'color','k','linewidth',1);
line([0 0],ylim,'color','k','linewidth',1);
xlabel('I');ylabel('Q');
title('Constellation plot for regular M-HQAM');
end
